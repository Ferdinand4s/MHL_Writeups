In the manifest, we see an intent-filter with a specified scheme and host.
![[image_2025-07-02_19-59-54.png]]
There is a check for the string UU0133 in the DAD4 file, which must match the result of the cd function, and a check to verify that the key passed via the intent (in Base64 format) matches the key hardcoded and encrypted within the app.
![[image_2025-07-02_20-04-07.png]]
The cd function simply retrieves the current date and formats it into a string.
![[image_2025-07-02_20-11-30.png]]
We create a DAD4.xml file.
![[image_2025-07-02_20-18-32.png]]
Then push it to the shared_prefs directory of the app on the device.
![[image_2025-07-02_20-19-21.png]]
Next, we locate the decrypt function.
![[image_2025-07-02_20-40-11.png]]
We write a Frida hook script.
![[image_2025-07-02_20-58-27.png]]
Run intent.
![[image_2025-07-02_20-59-04.png]]
After running it, we can see the decrypted secret.
![[image_2025-07-02_20-59-20.png]]
We encode the secret in Base64.
![[image_2025-07-02_20-59-45.png]]
Then launch the intent using the encoded secret.
![[image_2025-07-02_21-00-27.png]]
We see the result says “Success,” but it’s not the flag.
![[image_2025-07-02_21-00-50.png]]
Let’s try scanning memory. For that, we need a hex pattern.
![[image_2025-07-02_21-14-04.png]]
We write a Frida script to scan memory.
![[image_2025-07-02_21-21-41.png]]
Run the script, then trigger the memory scan function. The flag is retrieved.
![[image_2025-07-02_21-22-20.png]]