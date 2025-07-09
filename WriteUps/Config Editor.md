While analyzing the manifest, a field named intent-filter was found, containing a list of allowed schemes and MIME types.
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-34-21.png)
During the investigation of the intent handler, a call to the `loadYaml` function was discovered, which receives a URI from the intent.
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-36-01.png)
A detailed review of the loadYaml function revealed the use of the unsafe yaml_load function from the SnakeYAML library (https://www.labs.greynoise.io/grimoire/2024-01-03-snakeyaml-deserialization/).
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-41-42.png)
Upon studying the vulnerability, it became clear that it allows the creation of Java objects during exploitation. To maximize impact, the unused LegacyCommandUtil object was chosen, as it executes a command passed to its constructor upon initialization.
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-54-43.png)
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-49-32.png)
The file is opened.
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-49-56.png)
And in the logs, it is confirmed that the payload was executed.
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_18-50-03.png)
But there is nothing when i trying call payload with intent.

![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_19-21-35.png)![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_19-21-43.png)
![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_19-22-36.png)![Screenshot](Screenshots/ConfigEditor/image_2025-07-08_19-22-11 1.png)