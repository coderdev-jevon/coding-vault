# API
Date: 2026-07-21

## * ==Simple Definition==
	API stands for Application Programming Interface
- Application, a finished software with a job to do
- Programming, using written code not mouse clicks or manual typing
- Interface, defines how one software can talk to another

**API** is a standardized code that lets two different software programs exchange data automatically, it is also a Service Level Agreement (SLA) to specify the functional provider and expose the service path for its API users.

## * ==Web API==
One of the examples is the HTTP (Hypertext Transfer Protocol) request messages with XML or JSON response messages format.

#### ** SOAP and SOA to REST (design pattern)
SOAP and SOA are complicated to write and read as it wrapped in heavy XML text, while REST is a lightweight, simple standard for web APIs, uses regular HTTP rules (GET/POST/PUT/DELETE), returns clean JSON.

Every application which has CRUD(Create, Read, Update, Delete) operation has an API to create data, to get data, to update data or to delete data from a database.

#### ** API Endpoints
An endpoint is a web link where you send an HTTP request to do specific action.
1. `https://yourwebsite.com/api/add-text` → endpoint to save new text data (POST)
2. `https://yourwebsite.com/api/all-records` → endpoint to read all saved data (GET)
3. `https://yourwebsite.com/api/record/5` → endpoint to get only record number 5
#### ** World Wide Web (WWW)
It is a huge collection of web pages, images, data files, APIs stored on servers all over the world. It is one service that runs on top of the internet, like the shops and websites on the highway.

## * ==HTTP==
#### ** Client and Server
- Client is the one that asks for data.
- The client in this case is a browser, and the server (web server) is the place where you access the data.

 >HTTP Server and Web Server are not the same thing

	HTTP server is the software that understands HTTP protocol, while web server is a HTTP server that is built to serve static web content (HTMl, CSS, images)

#### ** Static vs Dynamic Data
Static data never changes automatically, stays identical for every user, every time you load it, while dynamic data changes based on request, user, time, database content, unique every load.

## * ==HTTP Structure==
#### ** Format of Request and Response Messages:
1. An initial line 
2. Zero or more header lines
3. A blank line (CRLF by itself)
4. An optional message body

#### ** Requests Headers
	get both request and response headers, first go to inspect -> network -> click any request name -> copy - copy request headers/ copy response headers

- **Initial Request Line**: method name, path of requested resource, HTTP version
- **Header Fields**: every line after the initial GET line (Accept, Accept-Encoding,etc) (**name: value**)
- **Blank CRLF**: CR (Carriage Return) or code \r that moves cursor back to the start of the line and LF (Line Feed) or code \n that moves cursor down one new line, act as separator between headers and body content
- **Message Body**: this is where user-entered data or uploaded files are sent to the server, if in the headers line contains message that describe the body, then HTTP message includes a body.

```
GET / HTTP/1.1 #Initial Request Line
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Accept-Encoding: gzip, deflate, br, zstd
Accept-Language: en-US,en;q=0.9,id-ID;q=0.8,id;q=0.7,da-DK;q=0.6,da;q=0.5
Cache-Control: max-age=0
Connection: keep-alive
Host: thirtydaysofpython-v1-final.herokuapp.com
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: none
Sec-Fetch-User: ?1
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/150.0.0.0 Safari/537.36
sec-ch-ua: "Not;A=Brand";v="8", "Chromium";v="150", "Google Chrome";v="150"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"

```
#### ** Response Headers
- **Initial Response Line**: HTTP version, response status code (200 OK Succeeded, 404 Not Found, or 500 Server Error)

>[!Status Code]

[HTTP Status Code](https://www.webfx.com/web-development/glossary/)

[HTTP Status Code Dogs](https://httpstatusdogs.com/)

```
HTTP/1.1 200 OK #Initial Response Line
Cache-Control: public, max-age=0
Content-Length: 1764
Content-Type: text/html; charset=utf-8
Date: Tue, 21 Jul 2026 06:05:39 GMT
Expires: 0
Nel: {"report_to":"heroku-nel","response_headers":["Via"],"max_age":3600,"success_fraction":0.01,"failure_fraction":0.1}
Pragma: no-cache
Report-To: {"group":"heroku-nel","endpoints":[{"url":"https://nel.heroku.com/reports?s=7y0%2FV0FOMaggnw20LtEeHXYfESwDrxzzeFGGLp68S%2BY%3D\u0026sid=1b10b0ff-8a76-4548-befa-353fc6c6c045\u0026ts=1784613939"}],"max_age":3600}
Reporting-Endpoints: heroku-nel="https://nel.heroku.com/reports?s=7y0%2FV0FOMaggnw20LtEeHXYfESwDrxzzeFGGLp68S%2BY%3D&sid=1b10b0ff-8a76-4548-befa-353fc6c6c045&ts=1784613939"
Server: Heroku
Via: 1.1 heroku-router
```

#### ** Request Methods
- GET: retrieve data using given URL
- POST: create and send new data to server
- PUT: modify or upload data
- DELETE: removes data

---

## * ==Additional==
#### ** Request Header Fields
``
```
- **Accept**: Tells the server what file formats your browser can read (HTML, images, XML, etc.)
  
- **Accept-Encoding**: Asks the server to send compressed data (gzip/br/zstd) to load faster
  
- **Accept-Language**: States your preferred page languages (English, Indonesian, Danish)
  
- **Cache-Control: max-age=0**: Forces the browser to load a fresh page, not use saved cache
  
- **Connection: keep-alive**: Keeps the network connection open to send more requests faster
  
- **Host**: The domain name of the website you are visiting (required for all HTTP/1.1 requests)
  
- **User-Agent**: Identifies your browser, Windows OS, and Chrome version to the server
  
- **Upgrade-Insecure-Requests:1**: Tells the server you prefer secure HTTPS pages
  
- `sec-ch-ua` series headers: Privacy-focused headers that tell the server your browser & device type without leaking personal data
  
- The Content-Type: header gives the MIME-type of the data in the body(text/html, application/json, text/plain, text/css, image/gif).

- The Content-Length: header gives the number of bytes in the body.
```

#### ** Response Header Fields
```
- **Cache-Control: public, max-age=0**
    Don’t save this page on your browser. Every reload must download a brand new copy.
    
- **Content-Length: 1764**
    The webpage code the server sends is 1764 characters long.
    
- **Content-Type: text/html; charset=utf-8**
    What the server sends is a normal website HTML page, and it supports all language letters.
    
- **Date: Tue, 21 Jul 2026 06:05:39 GMT**
    Exact time the server sent this page to you (global standard time).
    
- **Expires: 0**
    Old backup rule matching Cache-Control: this page is instantly expired, no saved copy allowed.
    
- **Nel: {...} & Report-To & Reporting-Endpoints**
    Heroku’s error log tools. If your page fails to load, the browser sends error messages to Heroku’s server for fixing bugs.
    
- **Pragma: no-cache**
    Outdated old-browser rule that also says “do not save cached page”.
    
- **Server: Heroku**
    Tells you this website is hosted on the Heroku cloud platform.

- **Via: 1.1 heroku-router**
    Your request first went through Heroku’s traffic router before reaching the actual website app.
```

## * For Review
```markdown
1. Define API and Web API
2. Why HTTP uses REST design over SOA and SOAP?
3. Explain the structure of request and response messages
```


#api #web #http #httpstatuscode
