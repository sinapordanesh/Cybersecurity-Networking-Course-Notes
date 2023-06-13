# 2_Web Application Security Testing with Google Hacking

# Introduction

- Sensitive data from web applications can be indexed by Google
- Google Hacking -> finding security weaknesses in web applications
- Directory listings and SQL syntax errors
- Publicly exposed backup files and internal server errors
- Sensitive data in the URL and insecure HTTP web pages
- Google Hacking Database
- Critical vulnerability in Microsoft Yammer social network
- How to prevent Google indexing from happening

# Google Hacking: Finding Directory Listings

## `site:{url} AND intitle:"Index of”`

This query is a Google search operator that allows you to find directory listings on a specific website. Here's how it works:

- `site:{url}` limits the search to a specific website. Replace `{url}` with the URL of the website you want to search.
- `intitle:"Index of"` searches for pages that have "Index of" in their title. This is a common title for directory listings.

So, when you combine these two search operators, you get a list of directories that are available on the website you specified. This can be useful for finding sensitive information that should not be publicly available, such as backup files or configuration files.

# Google Hacking: Finding SQL Syntax Errors

```sql
site:{url} AND ("mysql error with query" OR "mysqli connect" OR "mysqli query" OR "do mysal")
site:{url} AND (" [MICROSOFT][ODBC SQL" OR "[SQL SERVER]")
site:{url} AND ("PostgreSQL server: FATAL" OR "not a valid PostgreSQL result")
site:{url} AND ("ORA-00933:" OR "ORA-00921:" OR "ORA-00936:" OR "ORA-12541:" OR "[ODBC SQL")
```

Here's an explanation of each search operator for finding SQL syntax errors:

- `site:{url} AND ("mysql error with query" OR "mysqli connect" OR "mysqli query" OR "do mysal")`: This operator searches for MySQL errors that may have been caused by a syntax error in a query. The search term includes common phrases that may appear in an error message related to MySQL.
- `site:{url} AND (" [MICROSOFT][ODBC SQL" OR "[SQL SERVER]")`: This operator searches for errors related to Microsoft SQL Server. The search term includes common phrases that may appear in an error message related to Microsoft SQL Server.
- `site:{url} AND ("PostgreSQL server: FATAL" OR "not a valid PostgreSQL result")`: This operator searches for errors related to PostgreSQL server. The search term includes common phrases that may appear in an error message related to PostgreSQL server.
- `site:{url} AND ("ORA-00933:" OR "ORA-00921:" OR "ORA-00936:" OR "ORA-12541:" OR "[ODBC SQL]")`: This operator searches for errors related to Oracle SQL. The search term includes common phrases that may appear in an error message related to Oracle SQL.

By using these search operators, you can find pages on a specific website that contain SQL syntax errors. This can be helpful in identifying potential vulnerabilities in web applications and databases.

# Google Hacking: Finding Publicly Exposed Backup Files

## `site:{url} AND (ext: "backup" OR ext: "bak" OR ext: "old")`

`site:{url} AND (ext: "backup" OR ext: "bak" OR ext: "old")` is a Google search operator that searches for files with specific file extensions on a specific website. Replace `{url}` with the URL of the website you want to search. The operator `ext:` searches for files with a specific file extension. In this case, the search is looking for files with the extensions `.backup`, `.bak`, or `.old`. This can be helpful in identifying potentially sensitive information that may be stored in **backup files** that are publicly exposed.

# Google Hacking: Finding Internal Server Errors

## `site:{url} AND intitle: "500”`

This Google search operator is used to find pages on a specific website that contain an internal server error. The `site:{url}` operator limits the search to a specific website. The `intitle: "500"` operator searches for pages that contain "500" in their title. This is a common title for pages that return an internal server error. 

## `admin/.htpasswd`

`.htpasswd` is a file used for password protection in Apache web servers. It contains usernames and their corresponding hashed passwords. The `admin` directory is a common directory name used for administrative tasks in web applications. If the `admin` directory has a `.htpasswd` file, it means that the directory is protected by a password and only authorized users can access it. 

# Google Hacking: Finding Sensitive Data in URLs

## `site:{url} AND (inurl: "api" OR inurl: "key" OR inurl: "apikey")`

This Google search operator is used to find pages on a specific website that contain sensitive data in their URLs. Here's how it works:

- `site:{url}` limits the search to a specific website. Replace `{url}` with the URL of the website you want to search.
- `inurl: "api" OR inurl: "key" OR inurl: "apikey"` searches for pages that contain "api", "key", or "apikey" in their URLs. This can be helpful in identifying pages that contain sensitive data, such as API keys.

Using this search operator can help you identify potential vulnerabilities related to sensitive data being exposed in URLs.

- `site:{url}` limits the search to a specific website. Replace `{url}` with the URL of the website you want to search.
- `inurl: "api"` searches for pages that contain "api" in their URLs.
- `inurl: "key"` searches for pages that contain "key" in their URLs.
- `inurl: "apikey"` searches for pages that contain "apikey" in their URLs.

# Google Hacking: Finding Insecure HTTP Web Pages

## `site:{url} AND -inurl: "https”`

The query `site:{url} AND -inurl: "https”` is a Google search operator that allows you to find insecure HTTP web pages on a specific website. Here's how it works:

- `site:{url}` limits the search to a specific website. Replace `{url}` with the URL of the website you want to search.
- `inurl: "https"` **excludes** pages that contain "https" in their URLs. This means that the search will return pages that only use the HTTP protocol, which is less secure than HTTPS.

Using this search operator can help you identify potential vulnerabilities related to insecure HTTP web pages on a specific website.

# Google Hacking Database

- Google Hacking Database was created by Johnny Long
- This database includes special Google search engine queries (also known as Google Dorks)
- Google Hacking Database: [https://www.exploit-db.com/google-hacking-database](https://www.exploit-db.com/google-hacking-database)
- Johnny Long: "Google Hacking for Penetration Testers"
[https://www.blackhat.com/presentations/bh-europe-05/BH_EU_05-Long.pdf](https://www.blackhat.com/presentations/bh-europe-05/BH_EU_05-Long.pdf)
- You can find it helpful, when you want to learn more about Google Hacking and advanced Google search engine queries

# Case Study: Microsoft Yammer Social Network

- Access tokens to Microsoft Yammer social network were indexed by
Google
- Google search engine query -> access tokens -> unauthorized access to users' accounts
- This critical vulnerability was detected by Ateeq Khan from Vulnerability Laboratory Research Team
- It clearly shows the power of Google Hacking
- Report: [https://www.vulnerability-lab.com/get_content.php?id=1003](https://www.vulnerability-lab.com/get_content.php?id=1003)
    
    [Report.txt](2_Web%20Application%20Security%20Testing%20with%20Google%20Hac%20800561dd902f41a88d46f87f382fe31e/Report.txt)
    

# How to Prevent Google Indexing from Happening

- You don't want sensitive data from your web application to be publicly exposed on the Internet as a result of Google indexing
- Countermeasure: You should add the `robots.txt` file (in the root directory of your web-application) with the following content:
User-agent: *
Disallow: /
- Then, the web pages will not be indexed by Google.
- Sensitive data will not be exposed to everyone on the Internet.
- Other people will not be able to find this sensitive data by means of
Google Hacking

# Summary

- Sensitive data from web applications can be indexed by Google
- Google Hacking -> finding security weaknesses in web applications
- Directory listings and SQL syntax errors
- Publicly exposed backup files and internal server errors
- Sensitive data in the URL and insecure HTTP web pages
- Google Hacking Database
- Critical vulnerability in Microsoft Yammer social network
- How to prevent Google indexing from happening