In the application code, string concatenation was discovered when forming an SQL query. The password and address fields are encoded in Base64; however, the username is not encoded, making it potentially vulnerable to SQL injection attacks.
![[image_2025-07-07_20-33-35.png]]
To confirm that the field is not validated, we examine the class constructor where the variables are assigned. There are no validators present.
![[image_2025-07-07_20-35-02.png]]
When the username is passed into the constructor, it is also not validated.
![[image_2025-07-07_20-36-00.png]]
We craft a payload to register a user. To do this, we choose any username, encode the password and address in Base64, and set the isPro field to 1.
![[image_2025-07-07_20-30-41.png]]
After successful user registration via injection, we download the database.
![[image_2025-07-07_20-31-33.png]]
We open the database and confirm that the user has elevated privileges.
![[image_2025-07-07_20-31-51.png]]