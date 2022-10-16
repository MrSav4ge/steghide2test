# SQL Injection Challenge

# Introduction

Hi everyone and welcome to the DVWA SQL injection challenge. Here we are going to cover the basics of DWVA, what a SQL injection is, and finally how you will perform one on our console-based web application. 

## DVWA

First off let’s talk about DWVA. DVWA is an acronym for Damn Vulnerable Web Application. There are multiple different DVWA applications on the web that you can download and use but today we will be using our console-based web app to run SQL injections against.

## SQL and SQL Injections

Lets first begin by introducing what SQL is. SQL stands for structured query language and is the language used for accessing and manipulating databases. Databases themselves are an organized collection of structured information or data that web applications can use to help run their application. As for SQL injections they are a type of attack a malicious user can use to manipulate the database in unintended ways by writing their own SQL statements and queries to access information from the database they should not have access to. The way they can run these queries are by writing SQL queries into areas on the web application that take in user input such as entering a username or password. Now let’s move on to building our own queries to access information we shouldn’t have!

## Get Familiar with DVWA

When you first start the challenge you should notice a terminal page with a few commands that you can run. These commands are:

``` 
    view <page>
    enter [form]
    press {element}
    exit
```

There are descriptors for each command on screen. If you ever want to go back and reference these commands, you can type in the following command.

```
    home
```

To begin let’s start by viewing the index of pages available to you by entering 
```view index```. This should present you with a list of pages you can access which at this point should only be the login page. Use the view command again to enter this login page by entering 
```view login```. Now we have a few options from here we can enter in a username, enter in a password, or press login. First let’s enter some user credentials before we login. Start by using the enter command to access a username with the following command word for word. 
```enter username``` after entering in that command you should be on a new line, from here type in the name of the user then press enter lets start with using ```Avery```. Now we need to do the same entering process for the password, follow the previous steps and for the password enter ```12345```. Now that our credentials are entered, we need to use the login button, use the command ```press login``` to login with the given credentials. If successful you should be brought back to the index of pages you can view with a new page being available to us, namely the account page. View the account page using the view command and we will see the user’s details. This is the information we will be attempting to steal from a user that we do not have the password to.

## SQL Injection

Now let us try to login to another account in the DVWA database that we do not have access to. The username will be John, but we do not have his password. First if you are still on Avery’s account view the login page so we can enter the app as a new user. Now once again navigate to the login page and enter in ```John``` as the username. Pictured below is the code being used when entering in a user’s credentials.

```sql_statement = '''SELECT * FROM USERS WHERE NAME = '{username}' AND PASSWORD = '{password}'```

Here the line is the SQL statement being sent to the database in order to retrieve the correct user when the login button is pressed. The ```{username}``` will be substituted as John in this case and the ```{password}``` will similarly be substituted for anything we enter as the password. We need to trick the database into accepting this statement even if the password is not John’s actual password. To do this we will need to expand this statement to something that will always be true. In addition, notice the single quotation marks around the {password} we will need to account for these quotation marks as to not break the SQL statement’s syntax, if the syntax is incorrect the Query will not run, and we will not be able to access his account. Here are a few hints to get you started.

-	The AND implies both username and password need to be correct, however SQL statement also have an ```OR``` operator which means only one of the sides need to be true. You will need this in your password.

-	You can use single quotation marks ```‘``` in your password to properly close off values and keep syntax intact. (Each quotation mark will eventually need another to close it)

-	What is always true in mathematics? You can use numbers and the following in your password ```= , < , > ```

Once you have entered your password, attempt to login with the press command. If the password successfully ran a SQL injection you should be able to view John’s account details and his password to get your flag. If not the login page will reset and you will need to enter both the username and password again.

Good luck!
