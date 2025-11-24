This part is mainly discussed about how to do SQLi-RCE.

1.MySQL-SQLi-RCE:

Step1.Find the entry point of the web where we could inject SQL.Then, input random something
to this place.

Step2.Open Burpsuite to cache 'POST' request.Then, click 'Send to Repeater' to  find the furher
place where SQL could inject.

<img width="865" height="629" alt="image" src="https://github.com/user-attachments/assets/43fab1a4-f9e2-4b55-9ea8-b99a31e9ae12" />

According to above, we can suspect 'mail-list' where it could be implemented error-based SQL.So we type ' in this field to verify
it.If server responds 200 HTTP status code and error message to us, we could infer this field could be implemented SQL.

<img width="864" height="524" alt="image" src="https://github.com/user-attachments/assets/64ebe2d4-f8fc-40a2-8277-13abdce2afc7" />

<img width="864" height="547" alt="image" src="https://github.com/user-attachments/assets/5992f6a0-c4a1-470a-8c3e-b4e513446411" />


According to above, this field could be implemented error-based SQL.

Step3.Then, we implement union-based SQL on 'mail-list' to check the respond.

First, we determine the count of column. We implement 'order by 6-- -'.

<img width="835" height="625" alt="image" src="https://github.com/user-attachments/assets/571c5eb6-2f36-41ec-849e-cec03bbda37a" />

The respond is not error.Then, we implement 'order by 7-- -'.

<img width="864" height="662" alt="image" src="https://github.com/user-attachments/assets/d9a7eca8-4f2c-41ad-bf81-84a8a1d3825c" />

Above to the respond, we could get 'Unknown column '7' in 'order clause'' error message.So we could infer this table only has 6 columns.

Then,we implement 'union select 1,2,3,4,5,6-- -' to check what column has SQLi vulnerability.

<img width="830" height="727" alt="image" src="https://github.com/user-attachments/assets/167acec6-33dd-41a3-b086-278be85db1ea" />

Refer to above result, we could know the fiftth column has SQLi vulnerability.

Step4.Then,we could implement below MySQL-union SQLi that could trigger RCE on 'mail-list'.

<img width="864" height="517" alt="image" src="https://github.com/user-attachments/assets/11f24118-af00-4da0-93a1-ef05bccf63bd" />

According to below attack,we could infer this attack is similar 'File Uploading Attack'.And we need two things to notice:

.The schem for INTO OUTFILE isn't described as below:

*'union select "{?php system($_GET['cmd']);?}" ,null,null,null,null,INTO OUTFILE "/var/www/html/webshell.php",null.Because INTO OUTFILE only connects one string, not null.

*The attack proxy has the read/write rights on /var/www/html. If no, RCE would fail.

Step5.After implementing, we open monitor port 4444 to get the reverse shell from the target.

<img width="400" height="108" alt="image" src="https://github.com/user-attachments/assets/b8ea73c6-6435-4a6d-b8e4-d5ae9afc833f" />

Then,we browser to /var/www/html to run webshell with the RCE code that could reverse shell to us.In the mention, the RCE code should to be URL encoded.

<img width="865" height="79" alt="image" src="https://github.com/user-attachments/assets/41d2e330-a79a-46da-9d98-a5393be42b89" />

Finally, we get the target shell.

<img width="746" height="76" alt="image" src="https://github.com/user-attachments/assets/8f730d98-513d-4596-9e41-3f2a04f8afae" />


2.Postgre-SQLi-RCE:

Step1.Find the any entry point of the web where we could inject SQL.

Step2.Open Burpsuite to cache 'POST' request.Then, click 'Send to Repeater' to  find the furher
place where SQL could inject.

<img width="848" height="517" alt="image" src="https://github.com/user-attachments/assets/c619a0fb-af73-47fd-8296-696b0fea8c2a" />

According to above, we can suspect 'weight'、'height'、'age'、'gender' and 'email' where it could be implemented error-based SQL.So we type ' in each field to verify it.If server responds 200 HTTP status code and error message to us, we could infer it could be implemented SQL.

<img width="970" height="457" alt="image" src="https://github.com/user-attachments/assets/2087545b-b6fa-485f-bb1a-81be380c4313" />

According to above, we find the field-'height' that it could be implemented error-based SQL.Because as we type ' in this field to verify
it, the server responds error message to us, so we could infer this field could be implemented SQL.

Step3.After suspecting it, we could implement error-based SQL to get the version of Postgre DBMS.

<img width="948" height="380" alt="image" src="https://github.com/user-attachments/assets/375e70c3-d6bd-4293-bcac-5455dc628e01" />

However, we couldn't get any response from Postgre DBMS.

Step4.Then, we modify the way to implement Time-based SQL on 'height' to check it.

<img width="991" height="467" alt="image" src="https://github.com/user-attachments/assets/a5989db1-17d5-4474-8746-40e781eb73b3" />

As we finish implementing, we get response after 20 seconds.So, we could infer this field actually could be implemented SQL.

Step5.We open monitor port 4444 to get the reverse shell from the target.

<img width="400" height="108" alt="image" src="https://github.com/user-attachments/assets/b8ea73c6-6435-4a6d-b8e4-d5ae9afc833f" />

Then,we implement postgre-reverse shell command on the 'height' field.

<img width="979" height="481" alt="image" src="https://github.com/user-attachments/assets/9c4cb734-4b91-4852-bc83-fc8830e571c9" />

Finally, we get the target shell.

<img width="963" height="156" alt="image" src="https://github.com/user-attachments/assets/ee82e2c1-fbbc-4d00-b985-1fa47a6f4659" />

3.MSSQL-SQLi-RCE:

Step1.Also find the any entry point of the web where we could inject SQL.

Step2.Open Burpsuite to cache 'POST' request.Then, click 'Send to Repeater' to  find the furher
place where SQL could inject.

<img width="831" height="387" alt="image" src="https://github.com/user-attachments/assets/602c3fcc-b7dc-4f8b-8262-8e42d63130cd" />

According to above, we can suspect '_VIEWSTATE'、'_VIEWSTATEGENERATOR'、'_EVENTVALIDATION'、'UsernameTextBox'、'PasswordTextBox' and 'LoginButton' where it could be implemented error-based SQL.So we type ' in each field to verify it.If server responds 200 HTTP status code and error message to us, we could infer it could be implemented SQL.

(Because our target DBMS is MSSQL, so we need to do "UTF-16LE(1200)","Base64-Encode" and "URL-Encode" on our SQL command.Thus, ' should be url-encoded to %27)

<img width="825" height="398" alt="image" src="https://github.com/user-attachments/assets/e66b66ef-81a9-4e5e-9da4-a3e6ee3dc58f" />

After implementing,we can find the field-'UsernameTextBox' that could be implement SQLi.

Step3.After suspecting it, we could implement error-based SQL to get the version of MSSQL DBMS.

First,we need to url-encode on ';SELECT @@version;-- -.

<img width="534" height="407" alt="image" src="https://github.com/user-attachments/assets/7917c5ed-3a9e-4c1d-85dc-db47b47111af" />

Then,we inject this encoded command on the field-'UsernameTextBox'.

<img width="832" height="433" alt="image" src="https://github.com/user-attachments/assets/73498d04-74f5-481e-b824-72087f967579" />

However,we can't get response.So,we change our way to inject Time-based SQL on this field to check it.

We do url-encode on ';WAITFOR DELAY '0:0:20';-- -.

<img width="525" height="413" alt="image" src="https://github.com/user-attachments/assets/55602c43-1907-40f5-9e62-fd18c0f3bfb9" />

<img width="819" height="399" alt="image" src="https://github.com/user-attachments/assets/0f0a3585-f275-4670-a7c6-43732b9e2773" />

After injecting, we get response after 20 seconds.So, we could infer this field actually could be implemented SQL.

Step4.Now, we can do below process to do RCE:

Step4-1.First,inject below command to trigger xp_cmdshell.

<img width="751" height="607" alt="image" src="https://github.com/user-attachments/assets/7fcb5329-230c-4063-aefe-92641eb931ef" />

<img width="777" height="481" alt="image" src="https://github.com/user-attachments/assets/bcb7ec76-b856-4785-927b-71ffa2789574" />

Step4-2.Inject reconfigure command to re-configure it.

<img width="732" height="555" alt="image" src="https://github.com/user-attachments/assets/4dfc2cc6-4868-4852-9fc3-8e6bd299b419" />

<img width="753" height="422" alt="image" src="https://github.com/user-attachments/assets/28ec0bd1-bba2-4f4b-82c3-615dd8a700a6" />

Step4-3.Inject the command which could set 'xp_cmdshell' to 1.

<img width="771" height="617" alt="image" src="https://github.com/user-attachments/assets/f6f5875d-389f-458b-b8a7-28356a5b6878" />

<img width="804" height="526" alt="image" src="https://github.com/user-attachments/assets/631377f8-0b0c-4a37-b7fe-ffd03f32c227" />

Step4-4.Inject reconfigure command to re-configure it again.

<img width="770" height="587" alt="image" src="https://github.com/user-attachments/assets/70d95ed1-d70b-4144-b31b-b41307442496" />

<img width="802" height="521" alt="image" src="https://github.com/user-attachments/assets/abdcb8f9-de6d-4f5b-bce7-f5a670f74006" />

Step4-5.Then,we trigger the xp_cmdshell.

Step4-6.We open monitor port 4444 to get the reverse shell from the target.

<img width="350" height="84" alt="image" src="https://github.com/user-attachments/assets/6f24b2e7-d46b-44cb-89f7-7950ba2a7671" />

Then,we do below procedures to inject RCE command on the field-'UsernameText'.

Step4-5-1.Generating powershell RCE command which is encoeded by "UTF-16LE(1200)" and "Base64-Encode".

<img width="807" height="543" alt="image" src="https://github.com/user-attachments/assets/ad3eff51-6bd6-4146-bac3-8be42cfd0d69" />

Step4-5-2.Then,we do url-encode on 'EXEC xp_cmdshell ''-- -.

<img width="756" height="597" alt="image" src="https://github.com/user-attachments/assets/dfb1ca3c-fe6c-42c0-a172-b1b5e8c8c20f" />

(Sometimes, in SQLi, ; symbol shoud be added after ' symbol.But sometimes you don't need to add ; symbol after ' symbol.)

Step4-5-3.Afer above procedures, we wrap the powershell RCE command in the URL-encoded xp_cmdshell and inject it to the field-'UsernameText'.

<img width="778" height="484" alt="image" src="https://github.com/user-attachments/assets/a552c88b-5505-42cd-b50f-0fd64c79b80c" />

Step4-5-6.Finally,we send this SQLi to the target, then we get the shell of it.

<img width="794" height="447" alt="image" src="https://github.com/user-attachments/assets/f8e4664d-f715-49e4-9902-5fd334fdc373" />


4.MySQL-reverse shell resource:

https://medium.com/@tareshsharma17/simple-php-reverse-shell-061d4a6bd18d

5.MSSQL-reverse shell resource:

https://www.invicti.com/blog/web-security/sql-injection-cheat-sheet/

https://www.hackingarticles.in/mssql-for-pentester-command-execution-with-xp_cmdshell/

https://medium.com/@alokkumar0200/owning-a-machine-using-xp-cmdshell-via-sql-injection-manual-approach-a380a5e2a340

Above is the brief how to do MySQL,PostgreSQL and MSSQL RCE.
