In this report, we explained the mechanism of attacks using intent scheme URL, and three vulnerabilities  of  Android  browsers.  As  shown  in  section  4,  improper  handling  of  intent scheme  URL  may  result  in  significant  vulnerabilities  such  as  cookie  file  theft  and  UXSS from remote Web pages. 

The measure for such type of attack is to filter intent object (which is converted from intent scheme URL) more strictly, as shown in the following Java code. 

`// convert intent scheme URL to intent object 
Intent intent = Intent.parseUri(uri); 

// forbid launching activities without BROWSABLE category 
intent.addCategory("android.intent.category.BROWSABLE"); 

// forbid explicit call 
intent.setComponent(null); 

// forbid intent with selector intent 
intent.setSelector(null); 

// start the activity by the intent 
context.startActivityIfNeeded(intent, -1);` Finally, we would like to touch possible risks in other browser apps. As you know, there are many browsers for Android in the world, but we investigated only those listed in section 2. Browsers not mentioned in this paper might be vulnerable to attacks using intent scheme URL, as many browsers seem to be developed based on the vulnerable old stock browser
