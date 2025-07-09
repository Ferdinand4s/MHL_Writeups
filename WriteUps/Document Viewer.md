An intent-filter was found in the manifest, intended to handle URIs pointing to PDF files.
![[image_2025-07-08_13-14-18.png]]
Inside the intent handler, it’s clear that the URI is not validated to ensure it points to a legitimate PDF file. The function copyFileFromUrl is called, followed by a call to renderPdf.
![[image_2025-07-08_13-16-18.png]]
When copying the file, only the last segment of the URI is used. This is a vulnerable part of the code and, in theory, allows saving the file to a derived directory.
![[image_2025-07-08_13-17-37.png]]
To test the vulnerability, we trigger the intent using ../.
![[image_2025-07-08_13-12-27.png]]
The intent executed, and the desired file was opened.
![[image_2025-07-08_13-12-34.png]]
And as the cherry on top — the dynamic loading of the libdocviewer_pro.so library from the directory /data/data/com.mobilehackinglab.documentviewer/files/native-libraries/x86 (in my case, x86, but any other ABI may be used as well).
![[image_2025-07-08_13-18-31.png]]
The library itself is loaded during startup (onCreate), in the MainActivity class.
![[image_2025-07-08_13-19-24.png]]
Attack vector:
1. Write the payload in C.
![[image_2025-07-08_13-07-16.png]]
2. Compile the payload and place it locally on the attacker’s host in the directory ./data/data/com.mobilehackinglab.documentviewer/files/native-libraries/x86 with the filename libdocviewer_pro.so.
![[image_2025-07-08_13-07-41.png]]
3. Start a server that can decode URL-encoded characters such as %2F (/).
![[image_2025-07-08_13-09-30.png]]
4. Trigger the intent exploiting the path traversal.
![[image_2025-07-08_13-09-20.png]]
5. Restart the app and observe the proof of concept in the logs.
![[image_2025-07-08_13-10-07.png]]