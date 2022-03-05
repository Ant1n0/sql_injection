SQL injection Study

  
  Student Name： Peiran Sun， Yufeng Ge



  
  
  
  

# Intro:

Hello Everyone, My name is Yufeng Ge. Today I will be with my teammate Peiran Sun to discuss a very old yet still widely used exploit technique known as SQL injection.

  

![](https://lh5.googleusercontent.com/KcAD8ah1Jliztp5d63JLg1I2J83dqFaB5zk8pgZFgzoG07uZr6o5JAMhSIcz1cFTBfxVVxlF7u_OtoOodzV3-8rOET3KRFBv7e3c5rvOqkWo8MOIPm6q8giUwhtdvwM5LqgqBDwS)

https://ethos3.com/4-ways-to-make-your-message-stand-out/

  

As we step into the 21st century, the information on the internet grows exponentially each year. From user purchase history to business insight, one can almost say data is the most important asset in any industry. That's why almost every web application has some form of a database management system. They are used to manage and secure their precious business data.

  

I believe many of you have experience with SQL or an extension of standard SQL, such as MYSQL and PostgreSQL. It is the programming language used to communicate with the database from the backend.

Let's look at a typical SQL query

  

    INSERT INTO students (name) VALUES ('" + name + "');

Normally a front-end application will record the information from the user, and construct a SQL query to interact with the DBMS. This allows users to interact with the database without knowing any technical details.
It’s normally made up with two parts: the query itself, and input variable record information from the user.
  
However, a hacker could also exploit this model, by performing a technique known as SQL injection.

It’s normally made up with two parts: the query itself, and input variable record information from the user.

![](https://lh4.googleusercontent.com/Q8O599Glo5Aqw6P2tMcZvQwpmiHWmNY9aTJqYeNhnmGJiH2T9spAml9CUlbbH3AnaItPMWxPGrk_Ppr_lJZDUzHSkB4wdR3wyznS8zWrHhWhVuT-2920KWHAIhN9woD2Wz97sF4W)

(https://xkcd.com/327)

What is SQL injection:

So what is SQL injection, and how does it work?

  

Let's look back at a typical SQL query. You can see there are two parts, the query part and the user input part. The query part works like a vessel, carrying the information from the user to the DBMS. So what should we do if we want to do something bad under this model?

It is very simple, just feed malicious code as user input. By the nature of this model, your malicious code, or payload will be sent to the server and be performed on the DBMS. The effect of this technique depends greatly on three factors, the SQL query, the structure of the DBMS, and the type of payloads. And the result can be all the way from leaking sensitive information to destroying the DBMS completely.

  

The impacts of SQL injection:

  

This may look like a simple and easy way to hack. However, many major companies have been falling victim to it.

  

Here are a list of major companies who has been victims of SQL injections, and chances are, most tech company has been SQL injected, you can verify this using the CVE finding tool, just type the company name, and select SQL injection.vulnerability type

  

(https://www.cvedetails.com/vulnerability-search.php)

  

Just demonstrate how powerful one SQL injection can be,

This is from an interview with a hacker Group responsible for the data leak of Sony pictures Sony entertainment.

  
  

![](https://lh4.googleusercontent.com/uT8KUpLCypoC2EtvkyOJ_IijO0tYX6lHqIPjauKlRP9dxSAxRDj7Vq-EiBtQrkbE3j3VXJDrNlweZ2jdTrY7qQY-5BMD_XNv0wJ-zjvrAnfhsGTsjNGyv6KFYgND6SXm8gZWHIYu)

  
  

![](https://lh6.googleusercontent.com/qjoL8VClXmaxWov92R3WakZqd0JLBgb0xQ_Cre-2shDncKp3zzlO784Bw14nlT6fmYmoHTuesf3lT6PgjaAzNr61SO3JsGbaekzgcaOOTaTsf144gBhRDbqv6R9CG9pAZoJR_9Nx)

  
  

History(Background):（[https://www.vice.com/en/article/aekzez/the-history-of-sql-injection-the-hack-that-will-never-go-away](https://www.vice.com/en/article/aekzez/the-history-of-sql-injection-the-hack-that-will-never-go-away))

[https://owasp.org/Top10/](https://owasp.org/Top10/)

  

![OWASP publishes the Top 10 – 2017 Web Application Security Risks |  INCIBE-CERT](https://lh5.googleusercontent.com/jM4S2O7p8c0FgjKZAkjadIgKQnbE6jmFu24ULRfA61XcRZT7WasgYlw-07Dx9_Q0bwTyBDuRVsqoeiHZIBlbPpXVUuVsvk3G4SEUJVCrv--y_c6O5nYYkmBTPjAwD7ddMAjL6tvR)

![](https://lh6.googleusercontent.com/DtW66sGePRG1m0NNqoEIh_sST47sfnJ-Gs5UGDlwdUTPSVpB-DF7Hl554rmJEW7ySWAvge7_hsaGZeet6MZQO8hMWfqfLF7tcXNKuwpGe_i4YxQ1fLt1MTWet6w1HVrYimEt75t_)

SQL injection was first discovered and published in 1998 by Black hat hacker Jeff Forristal on a Microsoft SQL Server.

  

At that time, engineers from Microsoft did not even recognize this as a security problem, instead, they were calling this a normal behavior of SQL and asking Jeff not do things to prevent it.

  

What they didn't know is, they just witnessed the discovery of one of the most common vulnerabilities in history.

  

OSWAP is an organization focusing on the security of web applications, and they will publish the most common web vulnerabilities every 4 years. As you can see from the graph, SQL injection has always been in the top 3 since 2007.

  
  

Types of SQL Injections:

（https://www.imperva.com/learn/application-security/sql-injection-sqli/）

Let's talk about the type of SQL injection, basically,SQL injection has three types which are: In-band SQLi (Classic), Inferential SQLi (Blind) and Out-of-band SQLi. Although it is divided into three categories, these three types of SQL injection techniques are often interdependent.

So what is In-band SQLi（Classic SQLi）

In-band SQLi is one of the most common types of SQLi attack since it is really simple to implement.For this technique, attackers always use the same communication channel to do the attack and get the result which they need. There are two sub-variations of this method:

  

Error-based SQLi—Error-based SQLi has to depend on error messages thrown by the database server. Generally, hackers use the error message to snoop the structure of the database. （[https://www.youtube.com/watch?v=5ulehtDTuvE](https://www.youtube.com/watch?v=5ulehtDTuvE)). This is a very simple error-based example. It can be seen that after the attacker enters a meaningless string, the website responds to an error message to the attacker.Based on the "Diagnostic information" given in the error message. The attacker modifies the original select syntax through the input box so that the select condition is always true and the password requirement is avoided through the "#"symbol.

![](https://lh5.googleusercontent.com/8RBigV4j5SSqDmGtW-_pQTKE4-U5UT17YUXgwIsKF4B0NvDytA3d5XGSIl74DBTJV53yRUBH0Vv-7tebYVgtTAMEdEw1ahF8WhuKL2p4lt7vNiuPQESotkUPIIp0YLZEtMCr1eZE)

![](https://lh4.googleusercontent.com/GZ3oGu8KbNckmzDSJSYqgoazj_KUoMVUkfrNycmDHCMEjDAzQAPcsnUmQ73utW2hhCkoJaR8DVSukPPtU7NblMk99gRgtnhQnx-HyMb-c6GGoO1B6AQarWmbmKDC3P4bPrWcXNlY)

![](https://lh3.googleusercontent.com/bJ2OyRkKlnJjoOuNHtSNVZLPdM2JsomzEpYSab1s50kHPbozizgTihLMuOwpaiYfxq_0QR4TkglZSFJpE7wnM11GDaIxdZ5Ttb78GYij-v5mfjJTTMSWrgo576pumORHs3C_ao51)

![](https://lh4.googleusercontent.com/apbckYYtLKL5wcE-RysDUneZ1yQms8A5upDuDr8KKoNOW75RVYAciX-9sM-eJQzcyVbTZjWQHzIjaRkRZkbsqMHF8tk6tH9L-SnqOCyg7_KkiHF51KRZsVud7P_bGy6XwhxJs8Dt)![](https://lh6.googleusercontent.com/Emoh_5nw81MjvWIsZfx4oe7jCQ_Wy2FGmN1cQ6EN4ldd8R9JAm1qK99-3e5qGyTUyq8BXGaQzd1cOBWneZU8K4vsJy1Fmip7LammaPvdsuQYKtNs81dNcSNBVDK0Ku7MeHLduskZ)![](https://lh4.googleusercontent.com/tzaO4B_SSdJFHpNkZSEAFwgbGVmziGXvuHs1wToWyZsm_jBHXKIDXGI-gm3tXuBatkcg84D7yaguD6vwIhEzcLRG0hGO7mmsA9aDa7Lm2zWh7poQWMxhTkfVtJq3qwuLTfyj_OCc)

  

Union-based SQLi—The basic logic of Union-Based SQLi is using the Union SQL operator to combine the more select statements to let the information become one result.Then, return the information as a HTTP response. ([https://www.sqlinjection.net/union/](https://www.sqlinjection.net/union/))

There are two notice points which need to be considered. Based on the operator of Union, for two individual select statements, the number of columns must be the same.

  

The next is Inferential (Blind) SQLi

  

In short, Inferential SQLi is also called Blind SQLi, which means that the attacker cannot get information from the error message nor from the HTTP response. But attackers can send the data payloads and observe the response to infer the database structure or the data. Same as the In-band SQLi, Blind SQLi also has two sub-variations.

  
  

Boolean-based—that attacker could send a SQL query to the database to induce the database to return results. The information provided by the results is often related to the success of the query. Therefore, based on the result,attackers can get the information which they need. There is a boolean-based example, if we add a boolean command to the blue location payloads, we can infer some information from the messages provided by php code.

![](https://lh5.googleusercontent.com/1BPiZd0khtd0GGYjQdm9owZJTxL0v33bivYRw8n49S1s_tObwapYct46BqKhIyTycnCn4n6852655UjSDom-1nBZqqBmI_B5zYNgeC2jUIuhv2QCtibO3mgmqZzPxyd-k-oKQpEb)

The original select syntax is “Select first_name, last_name FROM users WHERE user_id = ‘$id’;”.

If we use input box to send the payloads in the picture,the syntax will be change like ![](https://lh5.googleusercontent.com/FYPRKUfdyw-rdmzNnbCLCqF9G8SsB6ZlI_5ckBagTN3RuYcXrW5ULa2Vt61hR-FUSUkB8CGdZ6BSTmu3CcqCQFXlWer7Q6M7iDzmlZvjucq9N0zePw21nU6opRjcEtVQ-Sg8ST57)this”Select first_name, last_name FROM users WHERE user_id = ‘1’ and length(database())=1#; ”

![](https://lh3.googleusercontent.com/FgAQMwIKymBx6cOYOC1ZzCgQR8FENqSLs64R-IvyulS5VLUzirJnbMbSR5GVDW5Jr5dnTlOysPh5JUSLj9zunnDsRBg1ButFDRh2dzNIQaT6G4ajz_ef6pB8vfgGprnkld4UgJd4)

Based on the message given by the php code the attacker could know that the length of the database is 4.

  

Time-based—The key to implement this injection is when sending SQL queries to the database, forcing the database to wait a period of time before responding. This allows the attacker to deduce whether the payloads used are true or false based on the length of the response.

  

The same is to get the length of the database, we can also solve it through time-based SQLi.

The original syntax is “Select first_name, last_name FROM users WHERE user_id = ‘$id’;”

If attackers send the payloads like this “1’ and if(length(database())=1,sleep(5),1) #”. Then the syntax of the code executed will become “Then the syntax of the code run will become "Select first_name, last_name FROM users WHERE user_id = '1' and if(length(database())=1,sleep(5),1) ". As a result,If there is an obvious pause after entering the payloads, it means that the database length attackers entered is the correct database length

  

Out-of-band SQLi

Compared with the first two SQLi techniques, Out-of-Band SQLi is less common. In general, when the attacker finds that the injection point of the application is very hidden and cannot be implemented by In-band methods, they will consider choosing the out-of-band method to do the injection.

  

Out-of-band SQLi is performed when the attacker can’t use the same channel to launch the attack and gather information, or when a server is too slow or unstable for these actions to be performed. These techniques count on the capacity of the server to create DNS or HTTP requests to transfer data to an attacker.
