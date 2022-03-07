# SQL injection Study

  
  Student Name： Peiran Sun， Yufeng Ge



  
  
  
  

# Intro:

Hello Everyone, My name is Yufeng Ge. Today I will be with my teammate Peiran Sun to discuss a very old yet still widely used exploit technique known as SQL injection.

  

![](https://lh5.googleusercontent.com/KcAD8ah1Jliztp5d63JLg1I2J83dqFaB5zk8pgZFgzoG07uZr6o5JAMhSIcz1cFTBfxVVxlF7u_OtoOodzV3-8rOET3KRFBv7e3c5rvOqkWo8MOIPm6q8giUwhtdvwM5LqgqBDwS)

[Pictrue](https://ethos3.com/4-ways-to-make-your-message-stand-out/)

  

As we step into the 21st century, the information on the internet grows exponentially each year. From user purchase history to business insight, one can almost say data is the most important asset in any industry. That's why almost every web application has some form of a database management system. They are used to manage and secure their precious business data.

  

I believe many of you have experience with SQL or an extension of standard SQL, such as MYSQL and PostgreSQL. It is the programming language used to communicate with the database on the server from the backend.

Let's look at a typical SQL query.

  

    INSERT INTO students (name) VALUES ('" + name + "');

The query is normally made up with two parts: the query itself, and some  input variables which record information from the user. For example, if name input from the user is Elaine, the query on the server will be like this:

    INSERT INTO students (name) VALUES ('Elaine');

  

So as a hacker, if we want to do some damage to the database, which part from this system could we take advantage of?

  

Remember we have two parts, query and input variable.

Of course we would choose to do something with the input variable, as it is the only communication channel we have to the server under this model.

That bring us to the definition of SQL injection, from Microsoft website:

> SQL injection is an attack in which malicious code is inserted into strings that are later passed to an instance of SQL Server for parsing and execution

[Definition](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-injection?view=sql-server-ver15)

The key point here is, malicious code is been inserted into the input. After that input is sent to the server, the SQL server will parse the input, and execute the malicious code.


# Little Bobby Tables:

[Reference](https://www.explainxkcd.com/wiki/index.php/Little_Bobby_Tables)
[Meme](https://xkcd.com/327)
![](https://lh4.googleusercontent.com/Q8O599Glo5Aqw6P2tMcZvQwpmiHWmNY9aTJqYeNhnmGJiH2T9spAml9CUlbbH3AnaItPMWxPGrk_Ppr_lJZDUzHSkB4wdR3wyznS8zWrHhWhVuT-2920KWHAIhN9woD2Wz97sF4W)


To better explain what is a SQL injection, let's look at a meme.

In short, the school is calling the mom because they are having a computer trouble,

  

They ask the mom if she really named her son **‘Robert'); DROP TABLE students;--’**.

  

And the mom said yes , she called him little bobby table in nickname.

  

The school them hope this mom are happy because they lost this year student’s record.

  

Apparently this mom has destoryed the school's database, but how?

Let's suppose the school has a query like this:

    INSERT INTO students (name) VALUES ('" + name + "');

I believe it is reasonable for a mom to name his son Robert, and that will be what's like on server side:

  

    INSERT INTO students (name) VALUES ('Robert');

However what if she really named his son 
**‘Robert'); DROP TABLE students;--’ ?**

The query will become:

    INSERT INTO students (name) VALUES ('Robert'); DROP TABLE students;--');

SQL does not know which parts are user input, which parts are the query, so it will parse this query. And in SQL semicolon separates each individual query, so the original query becomse three queries. Let's look at them one by one:

    INSERT INTO students (name) VALUES ('Robert');
    DROP TABLE students;
    --');
The first query looks fine, nothing wrong here. However, the second query completely drops the student table. After that, the third line , or '`--`' is used to commented out any code/query after wards. 
[Better explanation](https://www.explainxkcd.com/wiki/index.php/Little_Bobby_Tables)


#  The impact of SQL injection


This may look like a simple and easy way to hack. However, many major companies have been falling victim to it. Here are some big names on hall of shame: Yahoo, Zappos, Equifax, Epic Games, TalkTalk, LinkedIn, and Sony Pictures.....[Ref](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiiy-zg5K32AhU8FzQIHfKXCFgQFnoECBoQAw&url=https%3A%2F%2Fwww.malwarebytes.com%2Fsql-injection&usg=AOvVaw2TR9lB5bV2l_0c5Rcczz9T)  
![drawing](https://lh5.googleusercontent.com/0qHL3Hl4huefm2VVPE2akFZZ_Fb_7Fb1F1nZQp68SShH93KN3dGcGZYzmI1OsRqPIRXWkJdnnUhitl527SU1xLdTbH110lqE4MxKqENmY87FDkEtQ5xEjx9Fr_-_6utCSt0ev27W)

Chances are, almost every tech company has been SQL injected, you can verify this using the CVE finding tool from this [link](https://www.cvedetails.com/vulnerability-search.php), just type the company name, and select SQL injection.vulnerability type, you can see many tech company like Apple and Google has plenty SQL injection incidents.

 

  

Just demonstrate how serious one SQL injection can be,there was an interview with a hacker Group responsible for the data leak of Sony pictures Sony entertainment. This incident happens in 2014, and 1 million user password has been leaked from this incident.

> "SonyPictures.com was owned by a very simple SQL injection, one of the most primitive and common vulnerabilities, as we should all know by now," LulzSec said. "From a single injection, we accessed EVERYTHING."
> 
> "What's worse is that every bit of data we took wasn't encrypted," the group claims. "Sony stored over 1,000,000 passwords of its customers in plaintext, which means it's just a matter of taking it."

  
  


  
  

#  History(Background):

[Reference]([https://www.vice.com/en/article/aekzez/the-history-of-sql-injection-the-hack-that-will-never-go-away](https://www.vice.com/en/article/aekzez/the-history-of-sql-injection-the-hack-that-will-never-go-away))

[https://owasp.org/Top10/](https://owasp.org/Top10/)

  

![OWASP publishes the Top 10 – 2017 Web Application Security Risks |  INCIBE-CERT](https://lh5.googleusercontent.com/jM4S2O7p8c0FgjKZAkjadIgKQnbE6jmFu24ULRfA61XcRZT7WasgYlw-07Dx9_Q0bwTyBDuRVsqoeiHZIBlbPpXVUuVsvk3G4SEUJVCrv--y_c6O5nYYkmBTPjAwD7ddMAjL6tvR)

![](https://lh6.googleusercontent.com/DtW66sGePRG1m0NNqoEIh_sST47sfnJ-Gs5UGDlwdUTPSVpB-DF7Hl554rmJEW7ySWAvge7_hsaGZeet6MZQO8hMWfqfLF7tcXNKuwpGe_i4YxQ1fLt1MTWet6w1HVrYimEt75t_)

SQL injection was first discovered and published in 1998 by Black hat hacker Jeff Forristal on a Microsoft SQL Server.

At that time, engineers from Microsoft did not even recognize this as a security problem, instead, they were calling this a normal behavior of SQL and asking Jeff not do things to prevent it.

  

What they didn't know is, they just witnessed the discovery of one of the most common vulnerabilities in history.

  

OSWAP is an organization focusing on the security of web applications, and they will publish the most common web vulnerabilities every 4 years. As you can see from the graph, SQL injection has always been in the top 3 since 2007.

#  Types of SQL Injections:

[Reference1](https://www.imperva.com/learn/application-security/sql-injection-sqli/)
[Reference2](https://brightsec.com/blog/sql-injection-attack/)

Let's talk about the type of SQL injection, basically,SQL injection has three types which are: In-band SQLi (Classic), Inferential SQLi (Blind) and Out-of-band SQLi.

##  In-band SQLi（Classic SQLi）

In-band SQLi is one of the most common types since it is really simple to implement. For this technique, attackers always use the same communication channel to do the attack and get the result which they need. There are two sub-variations of this method(Error-based,Union-based)

###  Error based SQLi
Error-based SQLi has to depend on error messages thrown by the database server. Generally, hackers use the error message to snoop the structure of the database. （[reference](https://www.youtube.com/watch?v=5ulehtDTuvE)).

This is a very simple error-based example. It can be seen that after the attacker enters a meaningless string, the website responds to an error message to the attacker.Based on the "Diagnostic information" given in the error message. The attacker modifies the original select syntax through the input box.” the or operator” let the select condition is always true and the password requirement is commented through the "#"symbol.

![](https://lh5.googleusercontent.com/8RBigV4j5SSqDmGtW-_pQTKE4-U5UT17YUXgwIsKF4B0NvDytA3d5XGSIl74DBTJV53yRUBH0Vv-7tebYVgtTAMEdEw1ahF8WhuKL2p4lt7vNiuPQESotkUPIIp0YLZEtMCr1eZE)

![](https://lh4.googleusercontent.com/GZ3oGu8KbNckmzDSJSYqgoazj_KUoMVUkfrNycmDHCMEjDAzQAPcsnUmQ73utW2hhCkoJaR8DVSukPPtU7NblMk99gRgtnhQnx-HyMb-c6GGoO1B6AQarWmbmKDC3P4bPrWcXNlY)

![](https://lh3.googleusercontent.com/bJ2OyRkKlnJjoOuNHtSNVZLPdM2JsomzEpYSab1s50kHPbozizgTihLMuOwpaiYfxq_0QR4TkglZSFJpE7wnM11GDaIxdZ5Ttb78GYij-v5mfjJTTMSWrgo576pumORHs3C_ao51)

![](https://lh4.googleusercontent.com/apbckYYtLKL5wcE-RysDUneZ1yQms8A5upDuDr8KKoNOW75RVYAciX-9sM-eJQzcyVbTZjWQHzIjaRkRZkbsqMHF8tk6tH9L-SnqOCyg7_KkiHF51KRZsVud7P_bGy6XwhxJs8Dt)![](https://lh6.googleusercontent.com/Emoh_5nw81MjvWIsZfx4oe7jCQ_Wy2FGmN1cQ6EN4ldd8R9JAm1qK99-3e5qGyTUyq8BXGaQzd1cOBWneZU8K4vsJy1Fmip7LammaPvdsuQYKtNs81dNcSNBVDK0Ku7MeHLduskZ)![](https://lh4.googleusercontent.com/tzaO4B_SSdJFHpNkZSEAFwgbGVmziGXvuHs1wToWyZsm_jBHXKIDXGI-gm3tXuBatkcg84D7yaguD6vwIhEzcLRG0hGO7mmsA9aDa7Lm2zWh7poQWMxhTkfVtJq3qwuLTfyj_OCc)

  
###  Union-based SQLi

The basic logic of Union-Based SQLi is using the Union SQL operator to combine the more select statements to let the information become one result.Then, return the information as a HTTP response. ([reference](https://www.sqlinjection.net/union/))

There are two notable points which need to be considered. Based on the feature of the Union operator, for two individual select statements, the number of columns must be the same. And the Data type also needs to be compatible.

There is an example of union-based SQL injection. As we can see, the attacker uses “order by” syntax to get the correct number of columns.

  ![](https://lh3.googleusercontent.com/ggZSkwSXCvGF8PDE0N699T-QyyGLJPkkdQFZHY7EZX3NjYs2mpHoU-REPZupnIi1WAKLmeOOsvKFyoHvT4hF81XOK4RYd5CXijb-5lX3aCafSJrG9pjFbgVydorQEIsCd-70_bJU)![](https://lh6.googleusercontent.com/U7VF__KB6zvVOatPpW55l5dqrdilD_r6VfyXtPVazOjbYAKKJH9aXH0kfAy6mHQCUSv1FQCACkKtnb2EwqW4iqMRn-_lqUwAHlgnUo3-O85Pj_PBpc4xnfktrle16rWL0j7giPie)

Then we can see that when the attacker uploads the payloads, the data type is converted to Char so that the data type is compatible with the first statement.

As a result, you can see that the information of the database is shown onto the website page. [reference](https://www.youtube.com/watch?v=TlTMDw1KD_8)

  ![](https://lh3.googleusercontent.com/pptbm0Afp46mSPRIpmUCzFYGkItqoRG6tHEzc_baJxp49adBtrOjVWAAJ1QKQBqzEHlH7cAtE7Mxldef3ePhTjq8ytygLYqFQWYjl5aDQsJlzaUe_y_nQpkRBLXhizxHLnj7uyqi)

## Inferential (Blind) SQLi

  

In short, Inferential SQLi is also called Blind SQLi , which means that if attackers cannot get exact information from the error message nor from the HTTP response, they can send the data payloads and observe the response to infer the database structure or the data. Same as the In-band SQLi, Blind SQLi also has two sub-variations(Boolean-based,Time based).
  
  

### Boolean-based SQLi

Boolean based sqli means attacker could send a SQL query to the database to induce the database to return results. The information provided by the results is often related to the success of the query. Therefore, based on the result,attackers can get the information which they need. There is a boolean-based example, if we add a boolean command to the blue location payloads, we can infer some information from the messages provided by php code.

![](https://lh5.googleusercontent.com/1BPiZd0khtd0GGYjQdm9owZJTxL0v33bivYRw8n49S1s_tObwapYct46BqKhIyTycnCn4n6852655UjSDom-1nBZqqBmI_B5zYNgeC2jUIuhv2QCtibO3mgmqZzPxyd-k-oKQpEb)

The original select syntax is :

    Select first_name, last_name FROM users WHERE user_id = ‘$id’;

![](https://lh5.googleusercontent.com/FYPRKUfdyw-rdmzNnbCLCqF9G8SsB6ZlI_5ckBagTN3RuYcXrW5ULa2Vt61hR-FUSUkB8CGdZ6BSTmu3CcqCQFXlWer7Q6M7iDzmlZvjucq9N0zePw21nU6opRjcEtVQ-Sg8ST57)
If we use input box to send the payloads in the picture,the syntax will be change like  this

    Select first_name, last_name FROM users WHERE user_id = ‘1’ and length(database())=1#;

![](https://lh3.googleusercontent.com/FgAQMwIKymBx6cOYOC1ZzCgQR8FENqSLs64R-IvyulS5VLUzirJnbMbSR5GVDW5Jr5dnTlOysPh5JUSLj9zunnDsRBg1ButFDRh2dzNIQaT6G4ajz_ef6pB8vfgGprnkld4UgJd4)

Based on the message given by the php code the attacker could know that the length of the database is 4.

  


###  Time-based SQLi
The key to implement this injection is when sending SQL queries to the database, forcing the database to wait a period of time before responding. This allows the attacker to deduce whether the payloads used are true or false based on the length of the response.

  

The same is to get the length of the database, we can also solve it through time-based SQLi.

The original syntax is

 

    Select first_name, last_name FROM users WHERE user_id = ‘$id’;

If attackers send the payloads like this
 `1’ and if(length(database())=1,sleep(5),1) #`
 
Then the syntax of the code executed will become “Then the syntax of the code run will become 

    Select first_name, last_name FROM users WHERE user_id = '1' and if(length(database())=1,sleep(5),1) 

As a result,If there is an obvious pause after entering the payloads, it means that the database length attackers entered is the correct database length

  

##  Out-of-band SQLi

Compared with the first two SQLi techniques, Out-of-Band SQLi is less common. In general, when the attacker finds that the injection point of the application is very hidden and cannot be implemented by In-band methods, they will consider choosing the out-of-band method to do the injection.

  
Basically, Out of band SQLi normally depends on the database server’s ability to make the requests of DNS or HTTP to collect the data which hackers need. Some attackers use Oracle's http package to send requests to attacker-controlled servers to collect.([reference](https://www.acunetix.com/blog/articles/sqli-part-6-out-of-band-sqli/))
![](https://lh3.googleusercontent.com/0QAWQv-w6cPnkpQ_DvL_OR1MIbu2JpH7Er6q_gFuIstgMuR_JLvKgXSOcG_htPMLqtGliENPg_4nKEJH-hVkuNkOCOKAis8Tj1thc2Q32aVZpBCy8BMyyiiunrBEtEwXUYyVvvoN)

# What's more

Notice this article only explores 	SQL injection as a hacker tool to exploit web applications. If you want to know how to protect your web application from SQL injection, please have a look at [this](https://docs.microsoft.com/en-us/sql/relational-databases/security/sql-injection?view=sql-server-ver15).
