---
title:  "Budget-Report.ExE"
categories: [jekyll]
#tags: [jekyll]
---
Hello, today I will do a static, dynamic and network analysis of a malware called 'budget-report.exe'. I hope you enjoy reading it. Don't forget to take a snapshot! Because we don't know anything about file. It's can be a worm!
Let's Analyze :)

## STATIC ANALYSIS AND WINDOWS INTERNALS

I will use TridNet for getting information about the 'budget-report.exe'. We can see this file writing with C++ and it is a Executable file.

![png](/images/budget-report-malware/static/tridnet.png)

Then we can use PEStudio for getting more information about this file. We can see the first bytes hex '4D 5A'. that means it is a MZ so it is a Executable file.
And as we can see MD5 and SHA family Hashes.

![png](/images/budget-report-malware/static/PE-1.png)

```ruby
MD5 = 'd7cc6c987c68a88defdab3a59070777e'
SHA1 = 'C1BEEC6F6B8CC01FC093AC896D33F89F885E7D07'
SHA256 = '15cc3cad7aec406a9ec93554c9eaf0bfbcc740bef9d52dbc32bf559e90f53fee'
```

Let's look at the 'string' pages and select 'blacklist'. We can see RegSetValueEx, RegDeleteValue. That means when system rebooting, it will open yourself. We can see the 'socket' value. That means, this program connecting Internet.

![png](/images/budget-report-malware/static/PE-3.png)

We are not surprised, this program connecting a server. Let's see what is doing on Internet.

![png](/images/budget-report-malware/static/PE-4.png)

It is connecting, reading and closing the server. So the program does its job and leaves the server. This program using a lot of functions. Click the libraries section and see the blacklist and another functions.

```ruby
Blacklists API
wininet.dll
ws2_32.dll

Other Important APIs
kernel32.dll
user32.dll
```
This program using it 'T1112' Mitre Att&ck Techniques.

![png](/images/budget-report-malware/static/PE-5.PNG)

We need a more information about this file. Let's go to the Dynamic analysis and see what can we learn about this file.

## DYNAMIC ANALYSIS

I will use FakeNet, ProcMon, RegShot and ProcDot applications for dynamic analysis. I set the necessary configurations for these applications according to myself. Before executing the suspicious file, we must change the Network Connection. Because we know on static analysis, this program connecting Internet. Maybe it's can be a worm. Set the Network Connection 'NAT' to 'Host Only'.

Let's execute the file.

![png](/images/budget-report-malware/dynamic/1.PNG)

We observe that after running our 'budget-report.exe' file, it deletes itself. Let's look at the FakeNet, it is capture some packets. 

![png](/images/budget-report-malware/dynamic/2.png)

After waiting a few minutes, executable file repeating itself. We are capture the important informations and getting encoding data.

```ruby
Domain = "mbaquyahcn.biz"
POST / uan9Bau3LJ9 / HTTP
Port = 80
```
If we look at the RegShot report output, we can see where the malware is hiding itself. It's creating name on "S-1-5-21-..." 'HKU'. Then we can clearly see the persistence key '90c5b...' and this going to run 'ctfmon.exe'. 

![png](/images/budget-report-malware/dynamic/4.png)

When we look at the bottom of the report file; We see deleted, added files and folders.

![png](/images/budget-report-malware/dynamic/5.png)

```ruby
Files Added
C:\Users\pc\AppData\Roaming\12648430\ctfmon.exe
```
![png](/images/budget-report-malware/dynamic/6.PNG)

'budget-report.exe' delete itself and create a new executable file name of 'ctfmon.exe'. If we look at the ProcDot analysis, we can say clearly;
This program creating a batch file in Temp directory and delete itself again. Because in order for the 'ctfmon.exe' file to run, the .bat file needs to delete itself and trigger processes.

```ruby
C:\Users\pc\AppData\local\Temp\l12648430.bat
```
At the bottom, we can see that the file 'budget-report.exe' has been renamed to the filename 'ctfmon.exe'. Now we can say "This program is renaming itself to hide".

## NETWORK ANALYSIS AND VIRUSTOTAL

I will use WireShark to analyze the .pcap folder. Once the malware is run, we know the address it will visit, it goes to the domain 'mbaquyahcn.biz' and visits the directory specified by POST for data encoded in the HTTP protocol.

If we search on 'http' request in .pcap folder, then we can see all the information. It's same results with FakeNet.

![png](/images/budget-report-malware/dynamic/7.png)

And VirusTotal Results

![png](/images/budget-report-malware/dynamic/virustotal.png)

We have come to the end of static and dynamic malware analysis. What we know about the executable file?

- Firstly, 'budget-report.exe' remove itself and going to the this adress 'mbaquyahcn.biz/uan9Bau3LJ9' on 80 port.
- Secondly, it's creating a batch file for executing another program and delete itself again. The program name is 'ctfmon.exe'
- But we can see that 'budget-report.exe' and 'ctfmon.exe' are the same file. This means that the program wants to hide itself by changing its name.

 If you want to learn more about the analysis reports for this program, check the virustotal page with MD5 hash.

Thank you and I hope you like it :)