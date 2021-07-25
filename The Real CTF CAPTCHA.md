# The Real CTF CAPTCHA
If you’re a CTFer, you should be able to pass this CAPTCHA test.
Enter the letters you see in this picture.
![[real-ctf-captcha-example.png]]

For each attempt, a new image is generated with a unique string. In order to get the flag you must enter the correct string 25 times in a row. I manually decoded the 25 images using [stegsolve](https://github.com/zardus/ctf-tools/blob/master/stegsolve/install) . The text was hidden in one of the various color channels.

![[real-ctf-captcha-stegsolve.png]]

![[real-ctf-captcha-flag.png]]
