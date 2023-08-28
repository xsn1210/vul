Vulnerability plugin :EventON

Plugin download link: https://cn.wordpress.org/plugins/eventon-lite/

Vulnerability plugin version :2.1.7

Description :Download the EventON Lite plugin from the WordPress official website and install the latest version of the EventON Lite plugin. This plugin has an XSS vulnerability, that is, a cross-site scripting attack. The attacker will insert malicious JavaScript code into the web page (input form, URL, message board, etc.), and the payload is " oNmOuSeOvEr=prompt(1)//, replace the tab parameter in the url of /wp-admin/?page=eventon&tab=evcal_1 with the payload, which will trigger when the administrator/user visits, so as to achieve the purpose of the attack. The essential reason is that the server The data submitted by the user is not strictly filtered, causing the browser to treat the user's input as JS code and directly return it to the client for execution. What appears here is reflective XSS. Attackers can steal administrators, etc. by using reflective cross-site scripting attacks. User cookies, stealing clipboard content, changing web page content (eg download links), etc.
