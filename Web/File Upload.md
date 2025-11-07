This section is mainly talking ablout File Upload Attack.

1.File Upload Attack is uploading executable/non-executable file to web server to do further attack:disclose sensitive info
or RCE. And u don't know where the file is finally uploaded on the web server, so you need to "guess" it!!!

-----------------------------------------------------------------------------------------------------------------------------------------------------

2.Uploading Executable File:

Step1.Find the local point which could upload executable file to web server.

("/usr/share/webshells/" could provide many malicious executable files, so u could use them to upload.However,u should choice file
according to the skills web server use)

Step2.After uploading, u should find the file location. As u find out, u could use LFI attack to disclose sensitive info or RCE.

-----------------------------------------------------------------------------------------------------------------------------------------------------

3.Uploading Non-Executable File:

Step1.Choising local non-executable file u would like to upload. For example, authorized_keys.

Step2.After choising, determine whether file could upload to web server or not by Burpsuite.

Keep Working...
