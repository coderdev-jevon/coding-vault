# Chapter 17: Printing
Date: 2026-10-26

---
## ==🔵Keywords==
---
1. ==Local printer== - printer that is connected directly to your computer by USB.
2. ==Network printer== - printer that has its own network connection and IP address, any computer on the network can send jobs to it.
3. ==Print server== - computer or device that that sits between clients and printers.

---
## ==🔵 Printing on Linux==
---
To print, you need software to convert information from the application to language that printer can understand, in Linux, it is done by Common UNIX Printing System (CUPS).

---
##  ==🔵CUPS Overview==
---
It acts as print server for local and network printer.

---
## ==🔵Printing from Command-Line Interface==
---
`lp` stands for line printer
```bash
lp file.txt
lpr file.txt

lp -d printername file.txt # destination
lpr -P printername file.txt # Printer

lp -n number file.tx # times

lpoptions -d printer # set default

lpq -a # queue status

lpadmin # configure printer queue

lpstat -p # printers and status
lpstat -d # default printer
lpstat -a # available / accepting

cancel job-id # remove job
lprm job-id

lpmove job-id newprinter # move job 
```

---
## ==🔵Working with PostScript and PDF==
---
PostScript is standard page description language.

PostScript code -> PostScript interpreter -> Pixels on screen

---
## ==🔵Converting Between Postscript and PDF==
---
```
pdf2ps file.pdf
ps2pdf file.ps

pstopdf input.ps output.pdf
pdftops input.pdf output.ps

convert input.ps output.pdf
convert input.pdf output.ps
```
---
## ==🔵Viewing PDF Content==
---
`evince` is the most widely used program.

Evince means to show or reveal clearly.

---
## ==🔵Manipulating PDFs==
---
```bash
qpdf # widely used
pdftk # older alternative to qpdf
gs # ghostscript, widely used, but a little complex
```
---
## ==🔵Using `qpdf`==
---
```bash
qpdf --empty --pages 1.pdf 2.pdf -- 12.pdf # merge 1.pdf with 2.pdf
qpdf --empty --pages 1.pdf 1-2 -- new.pdf # write only page 1 and 2 of 1.pdf

qpdf --rotate=+90:1 1.pdf lr.pdf # rotate page 1 of 1.pdt 90 degrees and save it to lr.pdf
qpdf --rotate=+90:1-z 1.pdf lr-all.pdf # rotate all of the pages

qpdf --encrypt mypw mypw 128 -- public.pdt public.pdf private.pdf # encrypt with 128 bits
qpdf --decrypt --password=mypw private.pdf file-decrypt.pdf # decrypt
```

---
## ==🔵Using `gs`==
---
Many tools use it underneath, useful when you hit PDF problems.
```bash
gs -dBATCH -dNOPAUSE -q -sDEVICE=pdfwrite -sOutputFile=all.pdf file1.pdf file2.pdf file3.pdf # merges file

gs -sDEVICE=pdfwrite -dNOPAUSE -dBATCH -dDOPDFMARKS=false -dFirstPage=10 -dLastPage=20\  
-sOutputFile=split.pdf file.pdf** # extracts page 10-20 into new pdf
```
#### ==Options Breakdown==
```bash
-sDEVICE=pdfwrite # result is pdf
-sOutputFile=all.pdf # output file is all.pdf
-dBATCH # exit when finished
-dNOPAUSE # no pause between pages
-q # quiet, no messages
-dDOPOFMARKS=false # don't copy PDF marks.
```
---
## ==🔵Using Additional Tools==
---
```bash
pdfinfo # extract info
flpsed # FLTK postscript editor, add data to ps file
pdfmod # GUI to modify pdf files
```