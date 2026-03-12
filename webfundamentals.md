# WEB FUNDAMENTALS -
DNS (domain name system) - way for us to communicate w/ devices on internet (like IP address but complicated to remember so use DNS which is the name like tryhackme.com is DNS for 105.25.10.119)

## Domain Hierarchy
> Divided into TLD (top level domain), second level domain, subdomain

### Top Level Domain is most right hand part of domain name
Like tryhackme.com TLD is '.com'
#### gTLD (Generic Top Level)
Tells the user the domain name's purpose like .org for organization, .edu for education but there is an influx of new gTLD
#### ccTLD (Country Code Top Level Domain)
Geographical puposes like.ca for Canada, .co.uk for UK

### Second Level Domain
tryhackme is second level domain for tryhackme.com. It's limited to 63 chars and can only use alpha, num, hypens.

### Sybdomain 
Is the left hand part separated by a perdio like admin.tryhackme.com and has the same restriction as second level domain.
Max length of domain is 253 chars.

## DNS Record Types - DNS aren't just for websites
### A Record: resolve IPv4 addresses
> 104.26.10.229
### AAAA Record: resolve IPv6 addresses
> 2606:4700:20::681a:be5
### CNAME Record: resolve to another domain name
> tryahckme has subdomain: shop.tryhackme.com that retusn CNAM shops.shopfy.com
> then another DNS request would be made to shop.shopify.com to resolve IP address
### MX: resolve to affress of servers (that ahndle the email for the domain being queried)
> MX response for tryhackme.com would be alt1.aspmx.l.google.com
> come w/ priority flag in the order to try the servers
### TXT: free text fields where text data can be stored
> list servers that hae authority to send an email on behalf of domain
> _acme-challenge.example.com TXT "token_value_here"

## DNS Request Path
1. requesting a domain name first looks into the computer cache to see if address was recently visited, if not request to *Recursive DNS Server* is made
2. *Recursive DNS Server* is given from ISP and contains local cache of recently visited domain names. if request isn't found, we go to internet root server
3. root server direct to the correct TLD server recognized from TLD of the domain
4. TLD server has record for where to find authoritative server and can look like this (or tryhackme.com is kip.ns.cloudflare.com and uma.ns.cloudflare.com.)
> authoritative server: responsible for storing DNS records for domain name + any updates and sends back DNS record to recursive DNS server which comes with TTL to tell how long the response should be saved for locally

## HTTP + HTTPS
stands for HyperText Protocol Transfer and it's a set of rules used for talking w/ web servers for transmitting data
stands for HyperText Protocol Transfer Secure, it's encrypted so it stops people for seeing data being transmitted & received and assures correct web server is being reached

### URL - Uniform Resource Locator
it's an instruction on how to access a resource on the internet. It has:
*scheme*: (http part) instructs what protocol to use for accessing resource
*user*: can put username/password into URL to login (will be before the second level domain with @ sign connecting them in the form user:password)
*host*: domain anme
*port*: port connecting to (80 for http, 443 for https) and it comes after domain name with : sign connecting them
*path*: file name/location
*query string*: extra info can be sent to requested path

#### Example Request:
GET / HTTP/1.1

Host: tryhackme.com
User-Agent: Mozilla/5.0 Firefox/87.0
Referer: https://tryhackme.com/

#### Example Response:
HTTP/1.1 200 OK

Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>

### HTPP Methods
GET Request: get info from web server
POST Request: submit data to webserver
PUT Request: submit data to update info
DELETE Request: delete info from web server 

### HTTP Status Code
100-199 - Information Response: first part of request has been accepted and continue sending rest of their request
200-299 - Success: request was successful
300-399 - Redirection: redirect request to another resource which can be a different webpade or website
400-499 - Client Errors: error in the request
500-599 - Server Errors: error on the server side and big problem with server handling request


### Request Headers - headers sent from client to the server
*host*: web servers can host multiple websites so by telling which one is good otherwise you'll get default website
*user-agent*: tell server your browser and version to format website for it bc some things are only available on some browsers
*content-length*: when sending data to web server in like a form, tell how much data to expect to ensure nothing is missing
*cookie*: data sent to server to remember yur info

## How websites actually work
frontend: browser renders website
backend:server that processes your request and returns a response

> In summary when visiting a website, the computer needs to know the IP address to talk to so it uses DNS. Then, it talks to the server using commands in HTTPS and then the server returns HTML, JS, CSS

### Load Balancers - ensure high traffic websites handle the load + provide failover just in case
when a request to a website is sent, it goes through load balancer first and then tbe server because load balancer might send it in a round-robin algo or weighted

### CDN - content delivery networks
allows the static files from a website to be hosted across thousands of servers over the world so the nearest server located physically can send the hoste drequest instead of from one acorss the other side of the world.

### WAF - web application firewall
protects webserver from acking or DOS attacks. Checks inlude:
- checking if request is from a browser or a bot
- checks excessive amount of web requests sent from a certain IP address so introduces rate limiting

## at the end, what is a webserver?
> software that listens for incoming connections & uses HTTP to deliver web content to clients
examples include apache, nodejs.
