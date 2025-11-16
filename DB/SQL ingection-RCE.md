This part is mainly discussed about how to do SQLi-RCE.

1.MySQL-SQLi-RCE:

Step1.Find the entry point of the web where we could inject SQL.Then, input random something
to this place.

Step2.Open Burpsuite to cache 'POST' request.Then, click 'Send to Repeater' to  find the furher
place where SQL could inject.

<img width="865" height="629" alt="image" src="https://github.com/user-attachments/assets/43fab1a4-f9e2-4b55-9ea8-b99a31e9ae12" />

According to above, we can suspect 'mail-list' where it could be implemented SQL.So we type ' in this field to verify
it.If server responds 200 HTTP status code and error message to us, we could infer this field could be implemented SQL.

<img width="864" height="524" alt="image" src="https://github.com/user-attachments/assets/64ebe2d4-f8fc-40a2-8277-13abdce2afc7" />

<img width="864" height="547" alt="image" src="https://github.com/user-attachments/assets/5992f6a0-c4a1-470a-8c3e-b4e513446411" />


According to above, this field could be implemented SQL.

Step3.
