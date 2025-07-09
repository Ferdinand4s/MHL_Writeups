While examining the manifest, I found a service, but it was not exported.

![image_2025-07-08_18-27-20.png](../Screenshots/CyclicScanner/image_2025-07-08_18-27-20.png)

In the code itself, a scanFile function was discovered containing a command injection vulnerability.

![image_2025-07-08_18-29-07.png](../Screenshots/CyclicScanner/image_2025-07-08_18-29-07.png)

The call to this function was located inside the handleMessage function, which also calls itself recursively through messages.

![image_2025-07-08_18-30-18.png](../Screenshots/CyclicScanner/image_2025-07-08_18-30-18.png)

The first (initial) message is triggered by changing the state of a toggle button.

![image_2025-07-08_18-31-18.png](../Screenshots/CyclicScanner/image_2025-07-08_18-31-18.png)

To exploit this, we create a file.

![image_2025-07-08_18-25-56.png](../Screenshots/CyclicScanner/image_2025-07-08_18-25-56.png)

And then activate the scanner.

![image_2025-07-08_18-26-05.png](../Screenshots/CyclicScanner/image_2025-07-08_18-26-05.png)

From the log output, it is evident that the payload was executed.

![image_2025-07-08_18-26-14.png](../Screenshots/CyclicScanner/image_2025-07-08_18-26-14.png)