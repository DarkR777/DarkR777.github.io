---
layout: post
title: DownUnderCTF_2025_Writeup
date: 18-07-2025
categories: [DownUnderCTF]
tag: [DownUnderCTF]

---


# 🐶 DUCTF 2025 - e-dog


## 🧩 Challenge Description

> e-dog has been alone in the downunderctf.com email server for so long, please yeet him an email of some of your pets to keep him company, he might even share his favourite toy with you.  
>
> He has a knack for hiding things one layer deeper than you would expect.

![our lonely dog](images/our_lonely_dog.png)

---



## 🪜 Step-by-Step Solution

---

### 📤 Step 1: Sending a Pet Image to e-dog

When we accessed the challenge link, it allowed us to **submit a file** via email to e-dog.

📸 *Screenshot – Upload Form or Initial Prompt*  
![sent email](images/sent_email.png)

We submitted a dog image (`dog.jpeg`) as our pet companion.

---

### 📥 Step 2: Getting the Reply 

After submission, we received an email file from e-dog:

```shell
Hi, E-dog gets quite pupset when they can't find their bone, especially when it's been a ruff day. Maybe we need to pull out a new one for them?
```

### step 3: view original message

  After we got the reply, I click on the three dots and then "show original". After clicking that it gave me raw file.

  ![raw email](images/raw_email.png)

### step 4: Found the flag

We successfully found the flag.....

```shell
DUCTF{g00d-luCk-G3tT1nG-ThR0uGh-Al1s-Th3-eM41Ls}
```

Thanks for your interest... See you again.........