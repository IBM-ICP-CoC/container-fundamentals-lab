# Communication between containers

In this section you will create a second application container (App2) that will communicate with the first (App1), and display information that it is getting directly from the first app.

1. Make sure the disk mapping version of the application is running.

2. Change to the top of the working directory where you created the first `app1` directory.  (if you are still in the `data` sub directory, then entering `cd ../..` should get you back there).  Verify this is the right directory by listing its contents (`ls`) where you should see a single directory called `app1`.

3. Create a new directory for App2 and change to it.
```shell
mkdir app2
cd app2
```

4. Edit the Dockerfile (identical to the one we used for App1).
```shell
nano Dockerfile
```
Use the contents:
```dockerfile
FROM php:7.2-apache
COPY index.php /var/www/html/
```
Save the file (Ctrl-O, Enter) then exit (Ctrl-X).

5. Determine your laptop's current IP address. This is required because we can not use `localhost` inside a container - because the container is the localhost! For one container to connect to another container it must know the IP address of the host and then it can use the agreed upon port and filename.

In a terminal window enter the following command to determine the locally assigned IP address.
```shell
ipconfig getifaddr en0
```

5. Create and edit the main `index.php` file.
```shell
nano index.php
```
Add the following contents:
```php
<h1>App2</h1>
The following is coming directly from App1:
<code>
<?php
  echo file_get_contents("http://###.###.###.###:8080/test/sample.html")
?>
</code>
```
Where `###.###.###.###` is replaced with your actual local IP address. (for extra credit how would you pass this information in as an environment variable?).

Save the file and exit the editor.

The PHP `file_get_contents` function, is a general purpose resource reader.  It can read local files or fetch HTTP resources.  Since we provided it with a filename whose *scheme* begins with `http` it used the HTTP protocol to request the resource from the HTTP server configured on port 8080 of the local machine (which is App1).  The resource `/test/sample.html` is the file created in the previous step.

6. You can change this file on you local filesystem, then verify that the change is reflected in both App1 and App2.

----
[Overview](README.md)
