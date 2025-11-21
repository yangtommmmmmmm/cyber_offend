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

Finally, we got the target shell.

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

Step3.After suspecting it, we could implement bypass-authentication based SQL to get the version of Postgre DBMS.

<img width="948" height="380" alt="image" src="https://github.com/user-attachments/assets/375e70c3-d6bd-4293-bcac-5455dc628e01" />

Then, we couldn't get any response from Postgre DBMS.

Step4.Then, we modify the way to implement bypass-authentication and Time-based SQL on 'height' to check it.

