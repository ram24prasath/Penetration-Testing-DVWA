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

## Security Level = Medium

In this level, developers has added a check to strip all the tags from the input of message field.

The normal stored xss attack would not work here.

![image](https://github.com/user-attachments/assets/9777c15b-24d3-4d54-a86a-ded1df6a0086)

The `<script>` and `</script>` will be stripped from the input and hence the script injection will fail but since this check is done only for
message field. We can try to inject the script in name input field.

First, insect the name field and change the length, increase it to say 50, then use the following script in the name field.

This will successfully carry out the stored XSS injection.

![image](https://github.com/user-attachments/assets/7ecb7989-23c3-49b1-81fe-f8dffbbbda18)

## Security Level = High

In this level, the developers have added additional input sanitization to the name field. 

```bash
$name = preg_replace( '/<(.*)s(.*)c(.*)r(.*)i(.*)p(.*)t/i', '', $name );
```
This removes any pattern resembling to `script` and replace them null ''.

Attackers can bypass this by crafting input tags other than script.

```bash
<img src/onerror=alert(document.cookie)>
```

![image](https://github.com/user-attachments/assets/29a37cac-0f5a-4a07-8c08-387b66b5a966)
