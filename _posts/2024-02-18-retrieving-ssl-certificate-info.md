---
layout: post
title: "Retrieving SSL Certificate Information With Python"
description: "Retrieving SSL Certificate Information With Python"
date: 2024-02-01
tags: [Scripting, Python, SSL]
---

If you're building or supporting a live service, SSL certificates and and their management will no doubt be something you find yourself involved with at some stage. Whilst in the modern cloud landscape there is a vast array of tooling for monitoring and managing the life cycle of SSL certificates. There may come a time when a slightly more primitive solution is the one that works best.

This post provides some detail on how to monitor SSL certificates using a small but helpful Python program.

We'll look at creating the script itself, or if you would prefer to just retrieve a copy you can do so via GitHub <span style="color:blue">[here.](https://github.com/Joshua-K1/py-ssl-check)</span>
 
<!--more-->

## Check if Python is installed
First, we need to check that the machine we are using has Python installed. This post will focus on the use of Python3 so each of the commands will include the `python3` notation.


### Mac
Open a shell prompt, such as `Terminal` or `item2` and run the below command.


```javascript
python3 --version
```
If the system has Python installed, the output will look as below.

```
Python 3.x.x
```
If nothing, or an error message stating Python cannot be found is returned. Then you need to install it.


**Install Via the Python Website**

Visit the [Python Website](https://www.python.org/downloads/macos/) and download the latest or required stable release. Once downloaded, locate and run the `.pkg` file. Once ran, follow the installer instructions until completed.


**Install via Homebrew**

Homebrew is a package manager for MacOS and Linux. Similar to APT and YUM, Homebrew provides a straightforward package management experience. For instructions on how to install Homebrew, visit their website <span style="color:blue">[here.](https://brew.sh/)</span>


To install Python via Homebrew, run the below command:

```javascript
brew install python3
```

Once installed, you can again verify the installation by running the below command in shell prompt:

```javascript
python3 --version
```


## Creating the script
Navigate to a directory of your chooisng and create a file called ssl-check.py.

```
cd ~/repositories
touch ssl-check.py
```

Once created, open the file in your preffered text editor and at the very top of the file add the below statements to import the libraries required by the script.

```javascript
import ssl, socket # Allows us to make SSL connections to an endpoint
from datetime import date # Allows us to manipulate date objects
from dateutil import parser # Allows us to parse date objects into strings 
from prettytable import PrettyTable # Allows us to generate formatted tables
```

Next, we define 3 separate arrays. 
```javascript
domains = ["google.com, youtube.com"] # Stores the domains we will test
alt_domains = [] # Stores the certificate SAN names
crts = [] # Stores crt objects
```

In the above code, the domains array has been populated with the `google.com` and `youtube.com` domains. Replace these with the domains which you need to test. These can be anything that has a HTPS service housing a certificate and anything that is resolvable by DNS.


Next we define a Certificate class. For each domain tested, we will generate an object of the Certificate class which will store the pieces of information we retrieve.

```javascript
class Certificate:
    def __init__(self, name, san, expire, days_left, common_name):
        self.name = name
        self.san = san
        self.expire = expire
        self.days_left = days_left
        self.common_name = common_name
```

Next, we define our main function which houses a loop to iterate through the `domains` arrray and retrieve the certificate information of each domain held in the array.

```javascript
def main():
    # for each value in domains
    for domain in domains:

        # define the SSL session context
        # this is a helper function provided
        # by the ssl library to set secure
        # default settings.
        ctx = ssl.create_default_context()

		# create an SSL sockect and associate
		# it with the ctx (context)
        with ctx.wrap_socket(socket.socket(), server_hostname=domain) as soc:

			# open connection on port 
			# 443 with the domain held 
			# in the current loop 
			# iteration
            soc.connect((domain, 443))

			# uses socket helper function
			# getpeercert() to retrieve 
			# SSL certificate
            cert = soc.getpeercert()

            # create a dictionary object to unpack
            # values returned
            certificate_domains = dict(x[0] for x in cert['subject'])

			# create a var to hold the Common Name 
			# value returned
            issued_to = certificate_domains['commonName']

			# create an array to hold the SAN domains
			# as there are a number of SANs per cert, 
			# these are returned as an array from the dict
            certificate_alt_domain = cert['subjectAltName']

			# create an empty array to store
			# alt domain as it is retrieved
            x = []
            for alt_domain in certificate_alt_domain:
                alt_domain_lower = alt_domain[1]
                x.append(alt_domain_lower)

			# retrieve the expiration date and 
			# parse into a legible format
            res = parser.parse(cert['notAfter'], fuzzy=True)

			# retrieve the current date
            current_date = date.today()
            
            # minus the currne date from the 
            # expiration date and store as 
            # days left
            days_left=(res.date()-current_date).days

			# create an object (crt) of the Certificate class 
			# with the values retrieved
            crt = Certificate(domain, x, res.date(), days_left, issued_to)

			# append crt object to crts array
            crts.append(crt)

	# loop through each crt
	# object in crts array
    for crt in crts:

        # create a table using the PrettyTable libray with the 
        # Name, Common Name, Expiration and Days Left headers
        t = PrettyTable(['Name', 'Common Name', 'Expiration', 'Days Left'])

		# add the values of the crt object as a table row
        t.add_row([crt.name, crt.common_name, crt.expire, crt.days_left])

		# store the array returned
		# from crt.san as x
        x = crt.san

		# create a new table with the 
		# heading SANs
        t_s = PrettyTable(['SANs'])
        
        # for each value in x array
        # add as a row to table 
        for d in x:
            t_s.add_row([d])

		# print table t
        print(t)

		# print table t_s
        print(t_s)

if __name__ == "__main__":
    main()
```

Once the above has been added, the script is completed and can be ran with the below command:

```
python3 ssl-check.py
```

If you see an error such as the below, the libraries required by the script are missing.

```
Traceback (most recent call last):
  File "/home/leenux/repos/py-ssl-check/py_ssl.py", line 3, in <module>
    from dateutil import parser
ModuleNotFoundError: No module named 'dateutil'
```

To import the required libraries, create a new file called `requirements.txt` within the same directoy and within it add the below lines:

```
prettytable==3.8.0
python-dateutil==2.8.2
```

Once added, run the below command:

```
pip install -r requirements.txt
```

This file is also available within the repository <span style="color:blue">[here](https://github.com/Joshua-K1/py-ssl-check/blob/main/py_ssl.py)</span>

Now, when running the script the output should look as below:


```
+------------+--------------+------------+-----------+
|    Name    | Common Name  | Expiration | Days Left |
+------------+--------------+------------+-----------+
| google.com | *.google.com | 2023-10-09 |     54    |
+------------+--------------+------------+-----------+
+--------------------------------------+
|                 SANs                 |
+--------------------------------------+
|             *.google.com             |
|        *.appengine.google.com        |
|              *.bdn.dev               |
|        *.origin-test.bdn.dev         |
|          *.cloud.google.com          |
|       *.crowdsource.google.com       |
|       *.datacompute.google.com       |
|             *.google.ca              |
|             *.google.cl              |
|            *.google.co.in            |
|            *.google.co.jp            |
				
```
