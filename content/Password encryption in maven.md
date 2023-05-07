---
date: 2023-04-06T22:15:00+08:00
title: "Password encrytion in maven"
tags: ["Maven", "Step-by-step"]
author: "Brian Su"
description: "How to encrypt the password in maven?"
header_img: ""
draft: false
toc: "true"
---

## Metadata
- Links:
	- [Maven – Password Encryption (apache.org)](https://maven.apache.org/guides/mini/guide-encryption.html)

## How-to
- Use `mvn --encrypt-master-password` command to generate encrypted master password `mvn --encrypt-master-password <password>`.
- After executing the command, we will get the encrypted master password in string format. The master password will be used to encrypt other passwords.
- Store the password in the path: `${user.home}/.m2/settings-security.xml` with the following settings
	```xml
	<settingsSecurity>
		<master>/* password with curly braces */</master>
	</settingsSecurity>
	```
- After creating the master password, we could generate the encrypted server password by the command`mvn --encrypt-password <password>`.
- After generating the encrypted password, copy and paste the password into the `settings.xml`. It may look like:
	```xml
	<settings>
	...
		<servers>
		...
			<server>
				<id>my.server</id>
				<username>foo</username>
				<password>/* password with curly braces */</password>
			</server>
		...
		</servers>
	...
	</settings>
	```