Vulnerability plugin :EventON

Plugin download link: https://cn.wordpress.org/plugins/eventon-lite/

Vulnerability plugin version :2.1.7

Description :Download the EventON Lite plugin from the WordPress official website and install the latest version of the EventON Lite plugin. This plugin has an XSS vulnerability, that is, a cross-site scripting attack. The attacker will insert malicious JavaScript code into the web page (input form, URL, message board, etc.), and the payload is " oNmOuSeOvEr=prompt(1)//, replace the tab parameter in the url of /wp-admin/?page=eventon&tab=evcal_1 with the payload, which will trigger when the administrator/user visits, so as to achieve the purpose of the attack. The essential reason is that the server The data submitted by the user is not strictly filtered, causing the browser to treat the user's input as JS code and directly return it to the client for execution. What appears here is reflected XSS. Attackers can steal administrators, etc. by using reflected cross-site scripting attacks. User cookies, stealing clipboard content, changing web page content (eg download links), etc.

Test process:
1. Install the EventON plugin.
Download address: this website page https://cn.wordpress.org/plugins/ input plugin's name
EventON to download https://cn.wordpress.org/plugins/eventon-lite/

![image-xss1.1[EventON]](images/xss1.1[EventON].png)

![image-xss1.2[EventON]](images/xss1.2[EventON].png)

2. Navigate to the URL:
/wp-admin/admin.php? page=eventon&tab=evcal_1 or /wp-admin/admin.php? page=eventon&tab=evcal_2 or /wp-admin/admin.php? page=eventon&tab=evcal_3 or /wp-admin/admin.php? page=eventon&tab=evcal_4 or /wp-admin/admin.php? page=eventon&tab=evcal_5 and other pages

![image-xss1.3[EventON]](images/xss1.3[EventON].png)

3. Launch Burp Suite to capture network traffic. Use Burpsuite to capture and change packets for detection:

![image-xss1.4[EventON]](images/xss1.4[EventON].png)

4.Change the value of tab to "oNmOuSeOvEr=prompt(1)//, and send the modified url.
/wp-admin/admin.php?page=eventon&tab="oNmOuSeOvEr=prompt(1)//

Or change the value of the argument tab to "oNmOuSeOvEr=alert(document.cookie)// and send the modified url.
/wp-admin/admin.php? page=eventon&tab="oNmOuSeOvEr=alert(document.cookie)//

5. A pop-up window will appear on the web page, and an alarm box showing 1 will pop up, triggering XSS, indicating that there is cross-site vulnerability, recording the vulnerability, and stopping the test.

![image-xss1.5[EventON]](images/xss1.5[EventON].png)

A pop-up warning box showing cookies

![image-xss1.6[EventON]](images/xss1.6[EventON].png)

Attack steps:

1.Attackers create and test malicious URLs;

2.The attacker is sure that the victim loaded a malicious URL in the browser;

3.The attacker uses reflected cross-site scripting attacks to install keyloggers, steal victims' cookies, steal clipboard content, and change web page content (such as download links).

Attack method:

1. Use xss testing platform BlueLotus to steal cookies

2.Malicious links

3. Web phishing

4.Redirection implanted advertisement

Risk level: reflected cross-site presence in the application

Repair solution: 

For XSS cross-site vulnerabilities, the following repair methods can be used:

Overall fix: Validate all input data to effectively detect attacks; properly encode all output data to prevent any successfully injected scripts from running on the browser side. details as follows :

Input Validation: Validate the length, type, syntax, and business rules of all input data using standard input validation mechanisms before a certain data is accepted for display or storage.

Output encoding: Before data output, ensure that the data submitted by the user has been correctly encoded by entity. It is recommended to encode all characters instead of being limited to a certain subset.

Explicitly specify the encoding of the output: don't allow an attacker to choose an encoding (such as ISO 8859-1 or UTF 8) for your users.

Pay attention to the limitations of the blacklist verification method: just find or replace some characters (such as "<" ">" or keywords like "script"), it is easy to bypass the verification mechanism by XSS variant attacks.

Beware of normalization errors: Before validating input, it must be decoded and normalized to conform to the application's current internal representation. Make sure the application does not decode the same input twice. To filter the data submitted by the client, it is generally recommended to filter out special characters such as double quotes ("), angle brackets (<, >), or perform entity conversion on the special characters contained in the data submitted by the client, such as double quotes (") into its entity form &quot;, <corresponding entity form is &lt;, <corresponding entity form is&gt.
