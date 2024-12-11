# Email Analysis CTF Challenge 3

<h2>Description</h2>
In this email analysis challenge 3, I am a SOC Analyst at Global Logistics and I've been tasked to investigate a flagged email quarantined by the compan'ys email gateway. 


<h2>Languages and Utilities Used</h2>

- <b>https://github.com/MalwareCube/Email-IOC-Extractor</b>
- <b>Virustotal</b>


<h2>Environments Used </h2>

- <b>Unbuntu</b> 

<br />
<br />
Challenge 2 prompt.

![1) challenge task](https://github.com/user-attachments/assets/b723d86b-93db-41de-8698-7b35c8c84b63)

<br />
<br />
I used ioc python script from malwarecube to enumerate email sample headers.

![2) using python script to enumerate basic headers](https://github.com/user-attachments/assets/81dd0739-d363-4c84-a5f0-945a62cf3e64)

<br />
<br />  
I used whois.domaintools to find the email provider used to send this email. 

![3) the ASN of microsoft is the email infrastructure used to send the email](https://github.com/user-attachments/assets/452ad254-4a74-4917-93a1-26852069f0c5)

<br />
<br />
I used emldump python script to enumerate which index 5 containing the AR_Wedding_RSVP attachment. 

![4) run emldumpy script to enumerate the attached file](https://github.com/user-attachments/assets/eb9f9b09-858f-4f52-a48a-ee7e550d2f73)

<br />
<br />
Checking the attachment filehash on virustotal shows it being flagged as a malicious downloader. 

![5) conclusion, malicious attachment](https://github.com/user-attachments/assets/6f95182b-2bb0-464d-8478-fb5a396b680a)

<br />
<br />
Here I saved the malicious document for further static analysis. 

![6) bonus saved attachment](https://github.com/user-attachments/assets/2f92488c-91e2-4b27-a15f-39badb4af301)

<br />
<br />
Using oledump python script on the malicious document shows a macro in 'VBA/ThisDocument' index 3

![7) embedded macro in source 3](https://github.com/user-attachments/assets/056ce058-d060-4c87-b30f-d3723185ef33)

<br />
<br />
Running oledump python script with -s 3 -S flags to target the 'VBA/ThisDocument' containing the macro shows the malicious http link. 

![8) embedded script](https://github.com/user-attachments/assets/cae9b30f-3b7e-4c2b-8bc8-8faa22a740ce)

<br />
<br />
I used cyberchef to extract and defang the malicious URL in the macro script. 

![9) defanged url in macro script](https://github.com/user-attachments/assets/32f6d47d-0561-44b6-8bfd-b0b34e3b3e68)

<br />
<br />
I also enumerated the filename used by the macro to save the executable. In conclusion, this email is a malicious attempt to isntall a downloader into the user's system via downlaoder embedded macro. 

![10) file name used to save executable](https://github.com/user-attachments/assets/fbd9aa64-cba6-4a87-9282-02f17294d00a)
<br />
<br />
