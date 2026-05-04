## How I solved each of the labs

### SQLI:
SQL injection vulnerability in WHERE clause allowing retrieval of hidden data: added **'+OR+1=1--** into URL  
SQL injection vulnerability allowing login bypass:                             added **administrator'--** into URL  

### XSS:  
Reflected XSS into HTML context with nothing encoded: added **<script>alert(1)</script>** into the search bar  
Stored XSS into HTML context with nothing encoded:    navigated to a random blog and inserted **<script>alert(1)</script>** into the comment section and filled other fields with random names but expected format  
DOM XSS in document.write sink using source location.search: inserted **''><svg \onload=alert(1)>** into search bar  
DOM XSS in innerHTML sink using source location.search:      inserted ***img src='' \onerror=alert(1)>** into search bar
