This part is mainly discussed about how to do SQLi-RCE.

1.MySQL-SQLi-RCE:

Step1.Find the entry point of the web where we could inject SQL.Then, input random something
to this place.

Step2.Open Burpsuite to cache 'POST' request.Then, click 'Send to Repeater' to  find the furher
place where SQL could inject.

<img width="865" height="629" alt="image" src="https://github.com/user-attachments/assets/43fab1a4-f9e2-4b55-9ea8-b99a31e9ae12" />


