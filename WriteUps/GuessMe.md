While examining the manifest, I found an intent-filter with a defined scheme and host.
![[image_2025-07-07_19-46-03.png]]
When the intent is triggered, the isValidDeepLink function is called first. However, it’s sufficient to use either the mhl or https scheme to bypass the host verification against mobilehackinglab. Then, it checks whether the end of the incoming URI matches mobilehackinglab.com. In practice, this is an ineffective validation method, as it can be bypassed. After these checks, the loadDeepLink function is called, which simply opens a WebView using the provided URI.
![[image_2025-07-07_19-49-17.png]]
By default, the app opens index.html from the assets.
![[image_2025-07-07_19-50-00.png]]
Inside it, we see the use of the getTime function, which is exported from Java — making it possible to invoke it.
![[image_2025-07-07_19-50-24.png]]
At first glance, it might seem like there's nothing here.
![[image_2025-07-07_19-51-24.png]]
However, upon closer inspection, it's evident that the time parameter is not validated, making this part of the code vulnerable to injection.
![[image_2025-07-07_19-52-19.png]]
To begin, we send an intent with a payload to open arbitrary websites.
![[image_2025-07-07_19-55-36.png]]
And the payload successfully executed.
![[image_2025-07-07_19-55-48.png]]
To increase the impact of the vulnerability, we create our own HTML file that uses the vulnerable exported function.
![[image_2025-07-07_19-56-23.png]]
We start a server.
![[image_2025-07-07_19-57-09.png]]
Then, we send another intent using the address of our server.
![[image_2025-07-07_19-56-59.png]]
And as shown in the screenshot, the payload executed successfully.
![[image_2025-07-07_19-57-16.png]]