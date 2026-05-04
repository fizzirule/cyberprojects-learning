## How I solved each of the labs

### SQLI:
SQL injection vulnerability in WHERE clause allowing retrieval of hidden data: added <u>'+OR+1=1--<u>  
SQL injection vulnerability allowing login bypass:                             added <u>administrator'--<u>

### XSS:  
Reflected XSS into HTML context with nothing encoded: added <u> <script>alert(1)</script> <u> into the search bar  
Stored XSS into HTML context with nothing encoded:    navigated to a random blog and inserted <u> <script>alert(1)</script> <u> into the comment section and filled other fields with random names but expected format  
DOM XSS in document.write sink using source location.search: inserted <u> ''><svg onload=alert(1)> <u> into search bar  
DOM XSS in innerHTML sink using source location.search:      inserted <img src='' onerror=alert(1)> <u> into search bar
