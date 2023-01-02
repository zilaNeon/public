### Opera mobile for Android cookie theft

Opera browser’s filtering step is completely missing. Therefore, Web pages in Opera are able to launch any private activity of Opera  via intent scheme URL. An example of the attack code is as the following.

> `<script> 
location.href = "intent:#Intent;S.url=file:///data/data/com.opera.browser/app_opera/cookies;component=com.opera.browser/com.admarvel.android.ads.AdMarvelActivity;end"; 
</script>` 

By  using  this  code,  attacker  can  launch  **"com.admarvel.android.ads.AdMarvelActivity"** activity which is a private activity of Opera browser. The attack URL contains a string extra **"url=file:///data/data/com.opera.browser/app_opera/cookies"** which is the location of the file storing cookies of Opera browser.

**AdMarvelActivity**  does  load  the  URL  (pointing to the cookie file)  in  JavaScript-enabled WebView  and  render it  as  HTML.  Thus,  malicious  **HTML/JavaScript**  in  the  cookie  file  is executed in the context of the cookie file. It means that attacker can steal whole content of the cookie file, if he taints the cookie file beforehand by the code as shown below.

> `<script> 
document.cookie = "x=<script>(javascript code)</scr"+"ipt>; path=/blah; expires=Tue, 01-Jan-2030 00:00:00 GMT"; 
</script>` 

We  reported  this  vulnerability  with  working  PoC  code  to  IPA  (Japanese  incorporated administrative  agency  for  information-technology  promotion)  on  November  2013. JPCERT/CC  (Japanese  CSIRT  organization  working  with  IPA)  reported  the  issue  to  the vendor,  and  the  fix  from  the  vendor  was  released  on  January  2014.  CVE-2014-0815  was assigned to this issue.
