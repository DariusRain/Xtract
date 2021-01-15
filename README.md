# Xtract


### What is xtract
- A tool for developers to exctract data from websites and store simutaineously
- Allow devs to write uniform text format from example below or as a package in any project
- Capabilites of outputing raw .csv or .json files for further analysis
    - Also in the future would like to add a feture to export to SQL or NOSQL databases

### Theories in question
Would love for Xtract to be a web application or a API at the minimum.  Problem is the webdriver client, and how that would be able to that on a server with no browser.
 Aware of [alternatives](https://www.guru99.com/selenium-with-htmlunit-driver-phantomjs.html) but still weary on asynchronous and or dynamic elements from Javascript.
If that can be implemented then I will have an API where developers can write "Xtract scripts" then recieve through file via various protocols.


### Dependencies
[Selenium web driver java client](https://selenium-release.storage.googleapis.com/3.141/selenium-java-3.141.59.zip)
[Chrome web driver](https://sites.google.com/a/chromium.org/chromedriver/downloads)

### Example of an Xtract script
(Note: Will have it so it accepts dictionaries and JSON, I just like this implementation 🤷‍♂️)

*Prototype pseudo version*
```txt
CONFIG
    URL: www.google.com
    DRIVER: <WEB_DRIVER_PATH> --headless:true
    FORMAT: CSV or JSON ***(Theory after could do CSV --sql or JSON --mongodb )***

SCRAPE
    SCOPE: div:nth-child(2) > div:nth-child(2) > a:nth-child(1) --dynamic 
        

        title: h1:nth-child(1) --required
        description: p#desc

        SCOPE-1/contact: div:nth-child(1) --dynamic required
            address: span#address
            website: a#site --attr:href
            phone: span#phone 
            email: span#email 

        SCOPE-1/social: div:nth-child(2)
            twitter: ...path...
            facebook: ...path...
            instagram: ...path...

    NEXT/button: ...PATH...
    or
    NEXT/url: /listing/{a} --a:0 end:INF a-increment:1 (Both are by default, so optional)
    or (By default)
    Next/none: none

```   

### Explainaition
A*n expected examlple output of this*
```json
// JSON
[

    {
        
        "title":"Brady's Shoe Store",
        "description": "All the shoes you can buy",
        
        "contact": {
            "address": "1400 Main Ave Ney York NY 08976",
            "website": "www.someshoewebsite.com",
            "phone": "212-123-1234",
            "email": "bradyshoes@zzox.com"
        },
        
        "social": {
            "twitter": "",
            "facebook": "",
            "instagram": "",
        }
    },
      {
        
        "title":"...",
        "description":"...",
        
        "contact": {
            "address": "...",
            "website": "...",
            "phone": "...",
            "email": "..."
        },
        
        "social": {
            "twitter": "...",
            "facebook": "...",
            "instagram": "...",
        }
    }

]
```
&nbsp;

```csv
|title             |description               |address                         |website                 |phone        |email               |twitter|facebook|instagram|FIELD10|
|------------------|--------------------------|--------------------------------|------------------------|-------------|--------------------|-------|--------|---------|-------|
|Brady's Shoe Store| All the shoes you can buy| 1400 Main Ave Ney York NY 08976| www.someshoewebsite.com| 212-123-1234| bradyshoes@zzox.com|       |        |         |       |
```