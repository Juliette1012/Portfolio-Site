---
layout: post
title: Write-Up [THM] Scripting
categories: [Write-Ups, TryHackMe]
tags: [TryHackMe, Python, Scripting, Cryptography, Security]
featured-image:  thm/scripting/theme.png
featured-image-alt: Scripting
---

It's a write-up about the room : [Try Hack Me - Room : Scripting](https://tryhackme.com/room/scripting)

# Task 1 - [Easy] Base64

* What is the final string?  

The script `task-1.py` decoded the string which is in the file `b64.txt` to get the final flag. This one has been base64'd 50 times.

## Script task-1.py

```
import base64

file = open("b64.txt","r")
flag = file.read()

code = ""

for i in range(0,50):
	code = base64.b64decode(flag)
	flag = code

print(flag)
file.close()
```

After executed the scipt `task-1.py`, we obtained : `b'HackBack2019='`.   So, the flag is **HackBack2019=**.

# Task 2 - [Medium] Gotta Catch em All

## Script task-2.py

```
import socket 
import sys
import time

host=sys.argv[1]
port = 1337
number = 0

while 1:
	try:
		s = socket.socket()
		s.connect((host,port))
		if (port == 9765):
			break
		old_port = port
		request = "GET / HTTP/1.1\r\nHost:%s\r\n\r\n" % host
		s.send(request.encode())
		response = s.recv(4096)
		http_response = repr(response)
		http_trim = http_response[167:]
		http_trim = http_trim.replace('\'','')
		data_list = list(http_trim.split(" "))
		port = int(data_list[2])
		print('Operation: '+data_list[0]+', number: '+ data_list[1]+', next port: '+ data_list[2])
		if(port != old_port):
			if(data_list[0] == 'add'):
				number += float(data_list[1])
			elif(data_list[0] == 'minus'):
				number -= float(data_list[1])
			elif(data_list[0] == 'multiply'):
				number *= float(data_list[1])
			elif(data_list[0] == 'divide'):
				number /= float(data_list[1])
		s.close()
	except:
		s.close()
		pass

print(number)
```

`python task-2.py ip_machine`

# Task 3 - [Hard]

## Script task-3.py

```
import socket
import sys
import hashlib

from cryptography.hazmat.backends import default_backend
from cryptography.hazmat.primitives.ciphers import (
    Cipher, algorithms, modes
)

host = sys.argv[1]
port = 4000

def AES_GCM_decrypt(key, iv, ciphertext, tag):
	associated_data = ''
	decryptor = Cipher(algorithms.AES(key), modes.GCM(iv,tag), backend=default_backend()).decryptor()
	decryptor.authenticate_additional_data(associated_data)
	return decryptor.update(ciphertext) + decryptor.finalize()

def SHA256_hash(hash_string):
        sha_signature = hashlib.sha256(hash_string.encode()).hexdigest()
        return sha_signature

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.connect((host,port))

s.send(b'hello\n')
data = s.recv(2048)
print(data)

s.send(b'ready\n')
ready = s.recv(2048)
print(ready)
checksum = ready[104:136]
hex_checksum = checksum.encode('hex')
print("checksum in hex: "+hex_checksum)

while 1:
	s.send(b'final\n')
	flag = s.recv(2048)

	s.send(b'final\n')
	tag = s.recv(2048)

	key = b'thisisaverysecretkeyl337'
	iv = b'secureivl337'
	tag = bytes(tag)
	ciphertext = bytes(flag)
	plaintext = AES_GCM_decrypt(key, iv, ciphertext, tag)

	hash_string = SHA256_hash(plaintext)
	if(hash_string == hex_checksum):
		print('flag is: '+plaintext)
		break

s.close()
```

`python task-3.py ip_machine`