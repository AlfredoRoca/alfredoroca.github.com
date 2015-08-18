---
layout: post
title: "Calculate checksum on Windows"
description: ""
category: [windows, checksum]
tags: [sha256, md5, checksum]
---
{% include JB/setup %}

CertUtil is a pre-installed Windows utility, that can be used to generate hash checksums:

    certUtil -hashfile pathToFileToCheck [HashAlgorithm]

HashAlgorithm choices: MD2 MD4 MD5 SHA1 SHA256 SHA384 SHA512

So for example, the following generates an MD5 checksum for the file C:\TEMP\MyDataFile.img:

    CertUtil -hashfile C:\TEMP\MyDataFile.img SHA256