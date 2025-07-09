In the application manifest, a receiver was found with the flag exported="true" and an intent-filter with the action MASTER_ON.

![image_2025-07-07_19-19-04.png](../Screenshots/IotConnect/image_2025-07-07_19-19-04.png)

Upon further investigation, it was revealed that an additional field key is required, containing a 3-digit PIN code. If the correct PIN is provided, a log entry confirms the match.

![image_2025-07-07_19-20-01.png](../Screenshots/IotConnect/image_2025-07-07_19-20-01.png)

We write a script to brute-force the PIN code, as there are no restrictions on the number of attempts.

![image_2025-07-07_19-17-51.png](../Screenshots/IotConnect/image_2025-07-07_19-17-51.png)

Brute-forcing in progress.

![image_2025-07-07_19-17-26.png](../Screenshots/IotConnect/image_2025-07-07_19-17-26.png)

Log output upon successful PIN match.

![image_2025-07-07_19-18-15.png](../Screenshots/IotConnect/image_2025-07-07_19-18-15.png)

Program interface after enabling all devices.

![image_2025-07-07_19-18-29.png](../Screenshots/IotConnect/image_2025-07-07_19-18-29.png)