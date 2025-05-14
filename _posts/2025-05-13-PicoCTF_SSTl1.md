---
layout: post
title: PicoCTF_SSTl1_easy
date: 13-05-2025
categories: [PicoCTF]
tag: [Easy CTF]

---

Welcome to DarkR7 blogs.....

# Heading

```shell
I am DarkR7...
```


# picoCTF 2024: SSTI1 Challenge Writeup

## 📌 Challenge Description

> Can you exploit this website? Try to get the website to evaluate a Jinja expression.  


> Link: http://rescued-float.picoctf.net:59626/
 


## 🧠 Understanding the Challenge

This is a **Server-Side Template Injection (SSTI)** challenge using the **Jinja2** template engine.

Our goal is to inject Jinja2 expressions to get the server to execute arbitrary code and ultimately leak the flag.



## 🛠️ Step-by-Step Solution

### 1. Open the Website

The page asks for input and returns it rendered back. This suggests it may be vulnerable to SSTI.

![Initial Site](images/Screenshot_2025-05-13_14_46_53.png)


![The site](images/Screenshot_2025-05-13_14_48_45.png)



### 2. Test for Injection

We enter a basic test string: 

**&#123;&#123;7*8&#125;&#125;**

If the site returns `56`, then SSTI is confirmed.

![SSTI Test](images/Screenshot_2025-05-13_14_51_15.png)


![test result](images/Screenshot_2025-05-13_14_51_21.png)



### 3. Try Accessing Built-ins

To escalate, we inject the following payload to access built-ins:


**&#123;&#123;''.class.mro[2].subclasses()&#125;&#125;**


This gives access to all subclasses, including `Popen`.





### 4. Find `subprocess.Popen` Index

We locate the index of `subprocess.Popen` subclass from the list and use it to execute code. Example:

**&#123;&#123;''.class.mro[2].subclasses()[&lt;index&gt;]("ls", shell=True, stdout=-1).communicate()&#125;&#125;**


Try commands like `cat flag.txt`.



### 5. Extract the Flag

Eventually, we find the flag using a working payload like:

**&#123;&#123;''.class.mro[2].subclasses()[&lt;index&gt;]("cat flag.txt", shell=True, stdout=-1).communicate()&#125;&#125;**



And finally...

![Flag Final](images/sst1.png)



## 🏁 Flag

picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_3066c7bd}




## 📚 Concepts Learned

- Server-Side Template Injection (SSTI)
- Jinja2 internals
- Python object hierarchy
- Remote code execution using template injection



## ✅ Tips

- Always test for SSTI using `{{7*7}}`
- Use introspection to access sensitive functions
- Be cautious with payload indexing; try printing small batches to locate targets like `Popen`

