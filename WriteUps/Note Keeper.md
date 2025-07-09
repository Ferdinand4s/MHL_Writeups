While analyzing the form, it was determined that the name field lacks proper length validation and is passed directly into the native parse function.
![[image_2025-07-07_16-23-35.png]]
Upon decompiling the native library, it was observed that a 100-character array is allocated for the name, followed by a 500-character array, which is passed directly to the system function for command execution. In this case, a buffer overflow attack seems plausible.
![[image_2025-07-07_16-24-03.png]]
Essentially, the payload string consists of 100 characters followed by the command to be executed.
![[image_2025-07-07_16-32-25.png]]
We write a payload in the application that outputs "Hello from note" to the console.
![[image_2025-07-07_16-31-45.png]]
Save it.
![[image_2025-07-07_16-32-42.png]]
The logs show the result of a successful attack.
![[image_2025-07-07_16-32-33.png]]