This section is mainly discussed about the cracking way for getting login account/password. 

If u crack out the login page, you could do below way to crack out login account/password.Specially, the login url for wordpress contains 'wp-login.php' or 'phpmyadmin.php'.

<img width="477" height="357" alt="image" src="https://github.com/user-attachments/assets/bfedac93-2b55-43a6-a80a-a4173639d8c6" />

<img width="1454" height="803" alt="image" src="https://github.com/user-attachments/assets/c0016c25-f9ae-48e8-9caf-5b4b40bea244" />

If we would like to crack account/password for above wp-login.php, we could use below ways:

1.BurpSuite Tool:

Step1.Enable your burpsuite tool.

Step2.After enabling, u submit account/password to wp-login.php. Then, u could observe below POST Request:

<img width="665" height="17" alt="image" src="https://github.com/user-attachments/assets/ef30f2be-ce72-48cd-919e-539b22b7f7ed" />


Step3.Then, right click on this request,click 'Send to Intruder'.
<img width="519" height="303" alt="image" src="https://github.com/user-attachments/assets/15cb413e-85ca-4d13-aa25-02b25a8eccfa" />


Step4.Into the Intruder interface, choice the account or password value u would like to crack. After choicing, click
'Add button'.

<img width="657" height="223" alt="image" src="https://github.com/user-attachments/assets/0e8204d7-faf2-477c-9eb1-2721f40d8301" />


Step5.Next, click 'Intruder->Payload', input the account/password (located in rockyou.txt) to test.
<img width="428" height="443" alt="image" src="https://github.com/user-attachments/assets/30763c5e-6b07-4c2c-bfe2-bd25328b4266" />


Step6.Finally, u could get the cracking result as belows:
<img width="539" height="238" alt="image" src="https://github.com/user-attachments/assets/9aad52b2-2452-495e-b021-b28b4e06c545" />
