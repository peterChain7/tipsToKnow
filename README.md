## 1. Stabilize your reverse shell
    SHELL=/bin/bash script -q /dev/null 
    Ctrl-Z <
    stty raw -echo 
    fg 
    reset  
    xterm
   
 #### OR
    python3 -c "import pty;pty.spawn('/bin/bash')"
    export TERM=xterm; export SHELL=/bin/bash
    CTRL+Z
    stty raw -echo;fg
## 2. Nmap scan script
    $ cat nmap-scan.sh 
    ports=$(nmap -p- --min-rate=1000  -T4 $1 | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
    nmap -sC -sV -p$ports $1
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
