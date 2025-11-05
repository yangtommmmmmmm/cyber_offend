This .md is for introducing how to trigger BurpSuite tool.

Step1.Trigger BurpSuite.

<img width="631" height="42" alt="image" src="https://github.com/user-attachments/assets/746e2216-de93-4e14-b8ef-754f41d17da0" />

Step2.Neglect below warning.

<img width="495" height="242" alt="image" src="https://github.com/user-attachments/assets/ec24e666-0170-4b1a-9616-92b98fbe8c3f" />

Step3.Directly click 'Temporary project'->'Next'.

<img width="458" height="289" alt="image" src="https://github.com/user-attachments/assets/984960cc-aafd-4256-b5ba-fd32eb7bba3c" />

Step4.Directly click 'Use Burp defaults'->'Start Burp'.

<img width="433" height="272" alt="image" src="https://github.com/user-attachments/assets/ee9c5c5d-24d7-4b4d-b02b-f162f28827e7" />

Step5.Finally, we could get the UI for BurpSuite.

<img width="497" height="301" alt="image" src="https://github.com/user-attachments/assets/7be6c293-06e5-4dc2-9f10-a1b9fa68993a" />

Step6.After triggering, we click 'Proxy'->'Intercept' to let BurpSuite to capture the message between the client and server.Then,
also inspecting what port BurpSuite use by clicking 'Proxy'->'Options'.

<img width="499" height="289" alt="image" src="https://github.com/user-attachments/assets/81157622-e0a0-4f3c-b65a-e89d1b1e2fca" />
<img width="599" height="211" alt="image" src="https://github.com/user-attachments/assets/3326db4d-737e-4df3-953d-0aa13746d4da" />

Step7.Then, logging to Firefox browser, modify the setting.

Step7-1.Input 'about:preferences#general' on the Firefox browser.
<img width="589" height="370" alt="image" src="https://github.com/user-attachments/assets/c377531d-62a9-470b-9db3-174a08b2f4b2" />

Step7-2.Scrolling down the mouse and you can find 'Network Settings' located in
below.

Step7-3.Click 'Network Settings', then click 'Connection Settings'. Finally. click
'Manual proxy configuration' to modify HTTP Proxy and SOCKS Host. The modified info shows below:

<img width="586" height="493" alt="image" src="https://github.com/user-attachments/assets/ced9946a-583c-4ef9-8cdf-aef54789ff7a" />


Step8.Finally, we could intercept the message between client and web server by clicking 'Proxy'->'HTTP History'.
<img width="613" height="122" alt="image" src="https://github.com/user-attachments/assets/cf0962f7-7c1a-4278-bcc5-e3f0c8f72beb" />
