# Ad Network
## Description
Ad Network (Web, Baby, 50 pts)
Author: Alexander Menshchikov (@n0str)
We are so tired of advertising on the internet. It feels like it breaks the internet. Try to follow the ad, try to follow its rules.
Adnetwork website
There is a flag 1337 redirects deep into the network..

## Attack
Using the description of the challenge, my team thought we had to follow 1337 redirects and that the content-length would also be 1337. 
I initially used Burp-suite to see what the response would be for the following query 
`http://cold.adnetwork-cybrics2021.ctf.su/adnetwork`. The response confirmed that is was indeed a 301 response and that it redirected to a url that looked similar to
`http://cold.adnetwork-cybrics2021.ctf.su/discover-hour-able-eat/over-maybe-expect/start-usually-fall/test-beat-seek`. 

## Python Script
I created a quick python script to the follow redirects and after the 1336th request, print the header and the content of the response. I ran into issues with the request library throwing an error after following 30 redirects. As a result,  I manually followed the redirects instead of allowing the requests library to handle it.
```
import requests

count=0
resp = requests.get("http://adnetwork-cybrics2021.ctf.su/adnetwork",allow_redirects=False)
while True:
        if count % 50 ==0:
            print(resp.headers['Location'])
            print(resp.status_code)
        if count ==1400:
			print("something went wrong")
			break
		if resp.headers['Content-Length']  != "1337" or count <1337:
            resp=requests.get(resp.headers['Location'],allow_redirects=False)
            count +=1
        if count >=1337:
            print(count)
            print(resp.headers)
            print(resp.content)
    
```
![[ad-network-flag.png]]

## After The Challenge
I saw a write-up  which had a simpler python solution. It turns out that you can change the max amount of redirects that the request library will follow before throwing an error which would have simplified the above code.
`requests.Session().max_redirects=xxxx`