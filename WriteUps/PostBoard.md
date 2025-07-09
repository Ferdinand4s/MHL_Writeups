In the manifest, we find an intent-filter with a specified scheme and host.
![image_2025-07-07_14-08-38.png](../Screenshots/PostBoard/image_2025-07-07_14-08-38.png)
While analyzing index.html, we notice a pieWe encode the payload.ce of code using innerHTML, which is vulnerable to XSS.
![image_2025-07-07_14-09-10.png](../Screenshots/PostBoard/image_2025-07-07_14-09-10.png)
We encode the payload.
![image_2025-07-07_14-48-47.png](../Screenshots/PostBoard/image_2025-07-07_14-48-47.png)
Send it using an intent.
![image_2025-07-07_14-48-58.png](../Screenshots/PostBoard/image_2025-07-07_14-48-58.png)
And indeed, the HTML tags were parsed.
![image_2025-07-07_14-49-07.png](../Screenshots/PostBoard/image_2025-07-07_14-49-07.png)
Further analysis reveals four functions exported to JavaScript, one of which invokes the runCowsay function.
![image_2025-07-07_14-49-49.png](../Screenshots/PostBoard/image_2025-07-07_14-49-49.png)
The runCowsay function executes the cowsay.sh script, but due to string concatenation, it is vulnerable to command injection.
![image_2025-07-07_14-50-14.png](../Screenshots/PostBoard/image_2025-07-07_14-50-14.png)
We encode the payload calling the vulnerable function in Base64.
![image_2025-07-07_14-46-26.png](../Screenshots/PostBoard/image_2025-07-07_14-46-26.png)
Trigger the intent with the encoded payload.
![image_2025-07-07_14-46-46.png](../Screenshots/PostBoard/image_2025-07-07_14-46-46.png)
And observe the result of a successful attack.
![image_2025-07-07_14-46-55.png](../Screenshots/PostBoard/image_2025-07-07_14-46-55.png)