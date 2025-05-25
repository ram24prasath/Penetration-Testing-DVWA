# Stored XSS

Stored attacks are those where the injected scripts is permanently stored on the target server, such as database, message forums, comment fields and 
visitor logs.

The malicious script is delivered to the victim when the user request the stored information from the server.


## Security Level = Low

Fill the details of the forum. In the Message field input the crafted script.

```bash
<script>alert(document.cookie)</script>
```

After submiting the record, we can immediately see the pop up alert.

![image](https://github.com/user-attachments/assets/e3aa966f-5208-4c32-bb3d-da6e0c01fd29)

Unlike, reflected XSS, this is stored permanently, everytime the page is loaded it created this alert pop up.

