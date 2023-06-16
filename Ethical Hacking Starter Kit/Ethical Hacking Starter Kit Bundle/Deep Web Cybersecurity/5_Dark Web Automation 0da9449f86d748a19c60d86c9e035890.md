# 5_Dark Web Automation

# Introduction to Python

# Onion Link Automation Using Python

```python
import requests 
import random 
import re

def scrape(newdate):
    yourquery = newdate
	
    if " " in yourquery:
        yourquery = yourquery.replace (" ", "+")
    url = "https://ahmia.fi/search/?q={}".format(yourquery)
    request = requests.get(url)
    content = request.text
    regexquery = "\w+\.onion"
    mineddata = re.findall(regexquery, content)

    n = random.randint(1, 9999)

    filename = "sites{}.txt".format(str(n))
    print("Saving to ... ", filename)
    mineddata = list(dict.fromkeys(mineddata))

    for k in mineddata:
        with open(filename, "a") as newfile:
            k = k + "\n"
            newfile.write(k)
    print("All the files written to a text file : ", filename)

    with open(filename) as input.file:
        head = [next(input_file) for x in range(5)]
        contents = '\n'.join(map(str, head))
        print(contents)

newdata = input("enter query: ")
scrape(newdata)
```

This is a Python script that automates the process of scraping onion links from [https://ahmia.fi/search/](https://ahmia.fi/search/) based on a query input by the user. The script uses the requests module to send an HTTP GET request to the search URL with the user's query. It then extracts all the onion links from the HTML content using a regular expression pattern, and saves them to a text file with a random filename. The script then reads the first 5 lines of the text file and prints them to the console.

To run the script, the user is prompted to input a query, which is then passed as an argument to the `scrape` function. The function replaces any spaces in the query with `+` signs to form a valid URL, and then performs the steps mentioned above.

Overall, this script demonstrates how Python can be used to automate web scraping tasks, and how regular expressions can be used to extract specific data from HTML content.

# Onion Crawler Using Python

```python
import requests 
import csv 
import re 
import time

def get_tor_session():
    session = requests.session()
    # Tor uses the 9050 port as the default socks port
    session.proxies = {'http': 'socks5h://127.0.0.1:9050', 'https': 'socks5h://127.0.0.1:9051'}
    return session

def public_test():
    # Regex pattern for matching numbers
    pattern = "(?:[0-9]{4}-){3}[0-9]{4}|[0-9]{16}"
    # URLs of the websites to crawl
    urls = ['pastebin.com/diff/E34JsqAy', 'pastebin.pl/view/0f9e7cc4']
    # Loop through the URLs and fetch the HTML content
    for url in urls:
        response = requests.get("http://{}".format(url), timeout=25)
        response.close()
        html_content = response.content

        # Search for the regex pattern in the HTML content

        matches = re.findall(pattern, html_content.decode("ISO-8859-1"))

        # Output the matching numbers
        print ("Matching numbers on {}:".format(url))
        for match in matches:
            print (match)
        with open('scraped_data.csv', mode='a') as file:
            writer = csv.writer(file)
            for match in matches:
                writer.writerow([match])

def onion_test(filename):
    # Regex pattern for matching numbers
    pattern = "(?:[0-9]{4}-){3}[0-9]{4}|[0-9]{16}"
    # URLs of the websites to crawl
    data = [line.strip() for line in open(filename, 'r')]
    urls = data
    # Loop through the URLs and fetch the HTML content
    for url in urls:
        time.sleep(5)
        try:
            response = darksession.get("http://{}".format(url), timeout=25)
            response.close()
            html_content = response.content
        except requests. ConnectionError:
            continue

        # Search for the regex pattern in the HTML content

        matches = re.findall(pattern, html_content.decode("ISO-8859-1"))

        # Output the matching numbers
        print("Matching numbers on {}:".format(url))
        for match in matches:
            print (match)
        with open('scraped_data.csv', mode='a') as file:
            writer = csv.writer(file)
            for match in matches:
                writer.writerow([match])

filename = input("Enter file of websites name: ")

#For public test, connent prints and onion_test(). For onion_test(), just comment public_test().  
print("Connecting To TOR")
darksession=get_tor_session()
print ("New IP Address is: {}".format(darksession.get("http://httpbin.org/in").text))
onion_test(filename)
#public_test()
```

The `onion_test` function crawls onion sites using a TOR proxy. It first reads in a list of onion URLs from a file. It then loops through each URL, sends an HTTP GET request to the site using the TOR proxy, and extracts all the matching numbers from the HTML content using a regular expression pattern. The function then prints the matching numbers to the console and appends them to a CSV file called `scraped_data.csv`.

The purpose of using a TOR proxy is to keep the user's IP address hidden and to make it difficult for the site to track the user's behavior. The 5-second sleep timer between each request is included to prevent the user from getting blocked by the site, as frequent requests could be seen as suspicious behavior. If a connection error occurs, the function simply moves on to the next URL.

The final functionality of the code is to crawl onion sites and extract specific data from the HTML content of these sites using regular expressions. This functionality can be useful for a variety of purposes, such as scraping data for research or analysis. However, it is important to note that web scraping can be illegal or unethical in certain situations, so it should be used responsibly and with caution.

- To run this code we need the `Onion Link Automation Using Python` code run before and pass the result of that code as the “website names file” when we run this code.
- May need to check your Tor proxy configs and make sure all ports numbers are correct

# Telegram Bot for Scraping Onion Links

```python
import requests 
import re, random 
import telebot

BOT_TOKEN = '' #add your bot token here

bot = telebot.TeleBot(BOT_TOKEN)

@bot.message_handler(commands=['start', 'hello']) 
def send_welcome(message):
    bot.reply_to(message, """Welcome to Dark Web OSINT/darkweb (search) Example: /darkweb credit cards Created By Sina 
                            """)
    
@bot.message_handler(commands=['darkweb', 'getonions'])
def send_welcome(message):
    bot.reply_to(message,"[+] Getting Links")
    data=message.text 
    newdata=data.replace('/darkweb')
    bot.reply_to(message, scrape(newdata))
    bot.reply_to(message,"[!] You Need TOR To Access ninon Links")

def scrape(newdata):
    yourquery =newdata
    #yourquery - "Croatia Index Of"

    if " " in yourquery:
        yourquery = yourquery.replace (" ", "+")
    url = "https://ahmia.fi/search/?q={}".format (yourquery)
    request = requests.get(url)
    content = request.text
    regexquery = "\w+\.onion"
    mineddata = re.findall(regexquery, content)

    n = random.randint(1, 9999)

    filename = "sites{}.txt".format(str(n))
    print("Saving to ...", filename)
    mineddata = list(dict.fromkeys(mineddata))

    with open(filename, "w+") as _:
        print ("")
    for k in mineddata:
        with open(filename,"a") as newfile:
            K = K+ "\n"
            newfile.write(k)
    print ("All the files written to a text file : ", filename)

    with open(filename) as input_file:
        head = [next(input_file)for _ in range (7)]
        contents= '\n'.join(map(str, head)) 
        print (contents)

    return contents

bot.infinity_polling()
```

This code block contains Python code for a Telegram bot that can be used to automate the process of scraping onion links from [https://ahmia.fi/search/](https://ahmia.fi/search/) using the `scrape` function from the first code block in this document.

The bot uses the `telebot` library to interface with the Telegram API. When a user sends a message to the bot with the `/darkweb` command followed by a query, the bot calls the `scrape` function with the query and returns the first 7 onion links found in the search results.

To use the bot, the user must first obtain a bot token and add it to the `BOT_TOKEN` variable in the code. The bot can then be run on a server or local machine to handle incoming messages from Telegram users.

Overall, this code demonstrates how Python can be used to automate web scraping tasks and how the `telebot` library can be used to create custom bots that interface with the Telegram API.