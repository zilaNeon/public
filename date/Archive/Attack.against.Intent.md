### Chrome for Android UXSS (Universal XSS)

Attack against Chrome is a bit more complex. Chrome for Android contains Java code like the following

`Intent intent = Intent.parseUri(uri); 
intent.addCategory("android.intent.category.BROWSABLE"); 
intent.setComponent(null); 
context.startActivityIfNeeded(intent, -1);`

In the second line, Chrome limits launched activities to those with BROWSABLE category. In  the  third  line  Chrome  forbids  explicit  call.  These  limitations  are  measures  against intent-based attacks

However,  these  measures  are  insufficient  and  we  can  bypass  these  via  "selector  intent" which is a bit explained in API document. 

Selector intent is a mechanism introduced in Android API level 15 (Android 4.0.3). It is an additional intent object that can be attached to a main intent object. If the main intent has a selector intent, Android  framework resolves the destination of the intent not by the main intent but by its selector intent.

Intent scheme URL can contain selector intent as shown below.

> intent:#Intent;S.XXX=123;SEL;component=com.android.chrome/.xyz;end

"SEL" part of the URL is the indicator of selector intent.

Chrome for Android delivers this intent to **com.android.chrome/.xyz** component, even if the component does not have the **BROWSABLE** category. Malicious Web pages can utilize this to  conduct  attacks  to  Chrome's  private  activities  (including  those  without  **BROWSABLE** category) 

Now  the  issue  is  whether  Chrome  has  private  (or  public)  activities  that  can  be  used  for significant intent-based attacks. During our research, we found that WebappActivity can be used to conduct UXSS (Universal XSS) attacks. An example of attack in JavaScript code is shown below.

> `<script> // open target web page (http://victim.example.jp/) in WebAppActivity0 
location.href = "intent:#Intent;S.webapp_url=http://victim.example.jp;l.webapp_id=0;SEL;component=com.android.chrome/com.google.android.apps.chrome.webapps.WebappActivity0;end";  

// a few seconds later, inject javascript payload into target web page 
setTimeout(function() {
     location.href = "intent:#Intent;S.webapp_url=javascript:(malicious javascript code);l.webapp_id=1;SEL;component=com.android.chrome/com.google.android.apps.chrome.webapps.WebappActivity0;end";
     }, 2000); </script>`

In the  above  code,  the  malicious  Web  page  explicitly  launches  **"com.google.android.apps-.chrome.webapps.WebappActivity0"** twice. This activity is a private activity, and it does not have the **BROWSABLE** category, but the Web page can launch this activity by using intent scheme URL with selector intent. 

The first launch in our PoC forces **WebappActivity0** to load target Web page, and the second launch injects malicious JavaScript code into the target Web page. This means that attacker can inject his JavaScript payload into arbitrary **http/https** Web pages (Universal XSS)

As far as we know, an old version of Chrome for Android (v.30.0.1599.92) is vulnerable to this UXSS  attack.  Newer  versions  are  no  longer  vulnerable,  because  WebappActivity  was modified to open the second URL in a newly created tab. However potential risks remains, because current version of Chrome still does not filter selector intent so that malicious Web pages can launch private activities of Chrome for Android.




