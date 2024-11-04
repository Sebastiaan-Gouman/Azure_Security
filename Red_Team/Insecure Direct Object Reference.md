# Insecure Direct Object Reference


## Objective

To use insecure direct object reference vulnerability to change another user's password with BurpSuite repeater option. 

## How it's done

In this application, the user supplied input is used to access object directly. This object is the unique identifier for the object, in this case, it's the unique user ID number. 
After creating a new user and going over to the profile page, it's possible to change the password for the user. When doing so, and checking the developer tools, we can clearly see the new password, and the user ID being the number 10. 

![Insecure Direct Object Reference1.png](..%2Fmedia%2FInsecure%20Direct%20Object%20Reference1.png)

Now we could ask ourselves, what would happen if we repeated this action, but with another user ID? Let's find out! To repeat this action I'm using BurpSuite.

In the BurpSuite browser I logged in once more, went over to the profile page and changed the password, but this time I captured and forwarded the request in BurpSuite. Now we can alter and repeat this action to see if we can change someone else's password.

![BurpSuite.png](..%2Fmedia%2FBurpSuite.png)

After sending this action to the repeater in BurpSuite I changed the information in it. The `id` is now the number 2, and the password is `root`. After sending this request, I receive the 200/OK response, and the data of the changed account. All that is left to do now is to see if this actually worked. 

![Repeater.png](..%2Fmedia%2FRepeater.png)

To see if this worked I take the email from the response, and the new password, and try to log in.
Here we can see the login attempt, using the newly set password on an account we don't own.

![Login.png](..%2Fmedia%2FLogin.png)

And here we go, using the Insecure Direct Object Reference method we changed the password for another user.

![Succes.png](..%2Fmedia%2FSucces.png)

This is great, but in a database of users we might want to search for a specific user to attack. 
Well we actually can, because this web application has another vulnerability!

While still logged in I went to the "User" page. In BurpSuite I turn the intercept on, and enter the name "John" in the search field. 
After that, I forwarded the request. BurpSuite now shows me the following data:

![SQLI.png](..%2Fmedia%2FSQLI.png)

Once again I sent this to the repeater, here I can alter the contents to initiate a SQL injection attack. 

```
"value":"hello' or '1'='1"
"authlevel":"' or '1'='1"
```

And once again the web application gives us a lot of information. Even though it isn't pretty, all user accounts are in here!

![SQLi result.png](..%2Fmedia%2FSQLi%20result.png)
