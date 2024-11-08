# Server Side Request Forgery Part 1


## Objective

In this attack I want to use the SSRF technique to fetch the environment variables from the _/proc/self/environ_ file.

## How it's done

A Server-Side Request Forgery (SSRF) attack involves an attacker abusing server functionality to access or modify resources.

First I log in and navigate to the Newpost page. 
This is where the attack will start, in the "Enter URL of image" field I will enter the following payload.

### Payload:
```
file:///etc/passwd
```

The password file (as the name suggests) is a critical file for the Linux operating system and obviously stores information about the users. 
If the server returns the file in response to my request, that will confirm the SSRF vulnerability.

After I upload the payload I'm notified that the file was uploaded successfully, and in response I can see the URL in the developer tools.

![Payload uploaded successfully.png](..%2Fmedia%2FPayload%20uploaded%20successfully.png)

Now with the URL copied from the developer tools I can download the file. 
It downloads as a `.png` file, but opening this with Notepad shows the results!
On Linux this can be done with the cat command:

``` 
cat <filename>
```

![password file.png](..%2Fmedia%2Fpassword%20file.png)

This confirms I can use an SSRF attack, so now to the good stuff, let's do this again but with another payload.
Once again I navigate to the Newpost page and paste the payload in the file upload field.
Using the developer tools I extract the URL and download the _/proc/self/environ_ file.

### Payload:
``` 
file:///proc/self/environ
```

Opening this file with either cat or Notepad shows the contents.
Doing this with the following command will print each variable on a new line, making it easier to read:

``` 
cat <filename> | tr '\0' '\n'
```

![proc_self_environ file.png](..%2Fmedia%2Fproc_self_environ%20file.png)