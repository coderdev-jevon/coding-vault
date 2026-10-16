# Chapter 14.3: Browsers, `wget`, `curl`

---
## ==🔵* Graphical and Non-Graphical Browsers==
---

Graphical: Firefox, Google Chrome, Chromium, Non-Graphical: `lynx`, `elinks`, `w3m`

---
## ==🔵* `wget`==
---
`wget` stands for "World Wide Web get"
This `wget` utility is a command line utility to download files and information. 

#### ==** Definition of Downloading a Page==
Open web page -> Ask server for a file -> Server send it back -> Browser then displays it (Downloading a page stops at step 3, to open the file, you need a browser)

#### ==** Download File by `wget`==
```bash
wget <url>
```

---
## ==🔵* `curl`==
---
`curl` stands for "Client URL", it is used to CLI tool to transfer data to or from the server using URL. -> It prints the output

#### ==** Using `curl`==
```bash
curl <url>
curl -o saved.html <url> # to save the content
```

---