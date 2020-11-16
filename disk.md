# Disk and Volume Mounting

In this section you will map a directory inside a container to a directory outside of the container.  These are called volumes, and it is the second way (other than environment variables) to pass information into a container (without having to rebuild the container).  Volume and Environment variable mappings are the main ways the Kubernetes ConfigMaps and Secrets work.


1. Terminate any locally running docker applications.
```shell
docker rm -f $(docker ps -a -q)
```

2. Create a separate directory for us to map to (this way we won't accidently mess up our existing application files).  Change in this directory.

```shell
mkdir data
cd data
```

2. With your text editor create a new HTML file.
```shell
nano sample.html
```

3. Add any HTML you want to the file.  For example:
```html
<h1>My new file</h1>
<p>This is a sample HTML file that exists outside of my container.  It is not a file that is stored in the container.
</p>
```
Save the file.

4. Start the application again, this time passing in a volume mounting argument.
```shell
docker run -d -p 8080:80 -e MY_VAR="Hey" -v $(pwd):/var/www/html/test app1
```
The volume mounting argument, like the port mapping argument, accepts a string separated with a color.  The part before the colon is the directory on the hostmachine (your laptop).  The part after the colon is where this directory will show up inside the container.  In this case the current directory (as determined by the linux print working directory `pwd` command), and which happens to be the directory `data that you created` is the external volume.  Internally this directory will appear as a subdirectory named `test` in the main HTML directory where Apache looks for files.

5. Test the volume mount by having an external browser request the file you created on the host machine (and did NOT rebuild into the container image).   Use the URL http://localhost:8080/test/sample.html.  

![vol1](vol1.png)

6. Now edit that text file again.
```shell
nano sample.html
```

7. Make some changes to the file that you will notice, then Save the file.

8. Refresh the browser window and you should see your changes.

This demonstrates and verifies that the content for this web page is coming from a file that exists on your laptop, and that is not part of the built container.  This is a way information can be provided to a container that has already been built, without having to rebuild it.

----
[Overview](README.md)