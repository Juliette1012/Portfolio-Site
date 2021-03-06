---
title: Ringzer0CTF File recovery
template: "post"
date: "2020-12-03"
draft: false
category: "Write-Ups, Ringzer0CTF, Cryptography"
tags:
  - "Ringzer0CTF"
  - "Cryptography"
  - "RSA private key"
social-image: "/media/ringzer0CTF/icon.png"
description: "It's a write-up about the challenge : [Ringzer0CTF - File Recovery](https://ringzer0ctf.com/challenges/49)"
---

It's a write-up about the challenge : [Ringzer0CTF - File Recovery](https://ringzer0ctf.com/challenges/49)

# Challenge 49 - File recovery 

## 1. Challenge 

The crypto challenge is a folder :
* flag.enc
* private.pem

## 2. Solution 

We have one cripted file and one private key.
The file private.pem contained the RSA private key :

```
-----BEGIN RSA PRIVATE KEY-----
MIICXAIBAAKBgQDFDxrLz/lBabo/JrRvKN47IRzUgm/LzG9zbn3g8HMnPIpy4ZOF
fhjblvb8iNeFMbUIDAT2QmsqDRJhHH7xUVfC6DiYB3YuKJC/RBIHzqlBsxWXI5DF
ikyS3yT6ThQap3JZEKE7fVXHHJmea4VrsRVhWG6ztoPYf+OfiMyzj0IV3QIDAQAB
AoGAX1QnSmGZ2yMijlpS/1Nt7nzeTY+sNZL4d4cELkUj799BusGVdAbET7aAVTp9
yFl7kiD+ZYNMBFO+iGwYnPUU1sPSlFcS1YNu2S+4ds2ym1VfZu2drTN5qUIGIm22
2mgyOG1CSx421Ns4X5qIexkQ1gOnqaBuD7Mi3D19c5mK66ECQQDlt99Jcw7Jh1Gd
TMy8cQ7EBI82YPedRP5SnAv0/sCIgcsBmbABO6WwCeS1BVjoicf+pPmIy3YkyiyO
8JIa9GJLAkEA25qwREClnm+2qIBRLal+pG8t7xZlEya+HrlX3ogThf/9GybfImzK
ZQagbom3sDmRTeu6PhDhu4XZS7D4gfIPdwJANlDrsupJrM0aNx9ZqZTx8NdDJZB3
+++8Urwi96Lk02IdJhu4yhHYc29jbIn/I7ywVT2c4wN4w+op7wJjCYyPUQJAaVEo
U7NFOlSNHwZa6DEvQSDowI7W7nZYG1f74gcUheEcu5bK0DGoZwbkjd6SL3uMSfhR
G07xUwOAEKLQq1ExRQJBAJouci7CVIbd8XqZEBaBAqIEVKCff+qHsHzoZo1ryog8
vIgevI9e/01CqyuKIRs9WmM+DU/QnZtLJHUqgkpSCag=
-----END RSA PRIVATE KEY-----
```

This is why, we used openssl to decrypt the cripted file : flag.enc with this private key.

```openssl rsautl -decrypt -inkey private.pem -in flag.enc -out flag.txt```

In the new file flag.txt we discovered the solution : **FLAG-vOAM5ZcReMNzJqOfxLauakHx**