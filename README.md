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
![image](https://github.com/user-attachments/assets/7ce9b849-e042-4bfe-9f79-7fe5240678d6)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/user-attachments/assets/f9bfbbf5-bb10-4373-8ff9-ca53ae10fa51)
Click on the menu Login/Register and register for an account
![image](https://github.com/user-attachments/assets/65751874-3079-41fd-9574-084c2ab8d722)

Click on the link “Please register here”
![image](https://github.com/user-attachments/assets/6346aaf5-08e2-4301-ae65-067b5aa690c1)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:
![image](https://github.com/user-attachments/assets/8dc01e26-caeb-4a11-98ee-ddc2c8e09abc)

Union-based SQL injection: UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below:

![image](https://github.com/user-attachments/assets/3fa658bf-ba2c-4dc7-8085-198dcf00c17a)

![image](https://github.com/user-attachments/assets/fa8a4ece-6a9d-42e3-b401-640b460719f7)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![image](https://github.com/user-attachments/assets/156275f2-9a66-436d-8785-7d0d8b962f4e)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

![image](https://github.com/user-attachments/assets/30a81264-2d9a-464d-b5f3-77bfe6759cdc)

The browser url of this info page need to be modified with the url as below: When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.As it is having 5 columns the query worked fine and it provides the correct resultInstead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5) 

![image](https://github.com/user-attachments/assets/5dec1e03-cdff-4703-8eb0-ae42868d8f4a)

The browser url of this info page need to be modified with the url as below: When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.As it is having 5 columns the query worked fine and it provides the correct resultInstead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/user-attachments/assets/8aec4ce1-2c45-48ea-a24f-81ad2dcf6224)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database. The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table. Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

![image](https://github.com/user-attachments/assets/08c5d942-e434-4afa-a15b-4f974b41cef2)




## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
