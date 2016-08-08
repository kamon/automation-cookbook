# Using Github Personal Access Tokens to access a repository from a production server

As a developer, on your own machine, you access your code repositories on Github using your credentials, 
but on a server host (VPS or cloud host such as Heroku or PythonAnywhere) you should not use your 
personal account's password or SSH keys.

Now, for productivity reasons or cases where we want to do continuous deployment, we may need to access our github 
repositories from a server host.

There are several options to solve the problem, but one that was easy for me is "Personal access tokens",
which can be used instead of a password for Git over HTTPS.

To create an access token for each server you need to deploy code to:

1. Go to your Github settings page, and click on Personal access tokens.

2. Click on "Generate new token", and complete the form by setting the right access scope. For example, you 
   may use the "repo" scope to allow accessing your public and private repositories from the server (read and write access).

3. Once you click on the "Generate" button, the token is generated, and you have to copy it in a safe place, as with a password.

Then on your server, you will be able to clone one of your repositories by providing the token instead of the password.

```
$ git clone https://github.com/your_username/your_app.git
Username: your_username
Password: your_token
```

As for user accounts, tokens can be deleted whenever you want. For security reasons, you should regularly check how and when
they are used (the Github "Personal access tokens" interface shows when each token was last used), and you should
delete any token that is no more in use.