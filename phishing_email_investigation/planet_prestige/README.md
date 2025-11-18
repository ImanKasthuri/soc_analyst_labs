# BTLO - The Planet Prestige Challenge

## Overview

- This write-up documents my investigation of a suspicious email that showed multiple indicators of malicious activity. During the analysis, I discovered Base64-encoded data and an attachment that claimed to be a PDF but did not match standard PDF characteristics. After decoding the content with CyberChef, I determined that the file was actually a ZIP archive containing three files with misleading or missing extensions.
This report outlines the tools, techniques, and findings from the investigation.
  
## Tools Used

- NotePad++
- CyberShef
- HXD
- Exftool
- PowerShell
- 7 Zip
  
## Email Analysis

1. From: "Bill" <billjobs@microapple.com>
- This sender address is not legitimate. The domain “MicroApple” is fake, and the attacker is attempting to impersonate a well-known company to appear credible.
2. spf=fail (google.com: domain of billjobs@microapple.com does not designate 93.99.104.210 as permitted sender)
- Google flagged the message as unauthorized. It did not originate from a mail server authorized by the claimed domain, which is a strong indicator of email spoofing.
3. Received: from localhost (emkei.cz. [93.99.104.210])
- Emkei.cz is a known email spoofing service commonly used by attackers to send fraudulent or impersonated messages.
4. Reply-To: negeja3921@pashter.com
- The reply-to address does not match the sender address. This mismatch often reveals the attacker’s actual inbox and is a clear sign of malicious intent.
  
 <img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%201.png?raw=true">
 
## Analysis Using CyberChef and File Signatures

- I used CyberChef to decode the Base64-encoded blocks found in the email.
- Using the Hex operation, I examined the first four bytes (magic numbers) of the decoded content to identify the file type based on known signatures.
- The second Base64 block was identified as a ZIP archive rather than a PDF, confirming the attachment was intentionally disguised.

<img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%202.png?raw=true">

<img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%203.png?raw=true">

<img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%205.png?raw=true">


## File Analysis

- I used HxD to examine the extracted files. Attackers often remove or alter file extensions to conceal the true file type.
- One of the files opened in Excel showed suspicious, unreadable content. After removing the cell formatting, I found hidden Base64 text embedded in the sheet—another clear sign of obfuscation.

<img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%204.png?raw=true">

<img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%206.png?raw=true">


## PDF Metadata Analysis

- I used ExifTool in PowerShell to inspect the metadata of the file GoodJobMayor.pdf.
- The metadata revealed additional information, including details that may indicate the attacker’s alias or identity.
<img src="https://github.com/ImanKasthuri/soc_analyst_labs/blob/main/phishing_email_investigation/planet_prestige/screenshots/Screenshot%207.png?raw=true">

## Commands Used

- exiftool -f "GoodJobMajor.pdf"

## What I Learned

- Email spoofing is easy to perform, especially with services like Emkei.cz. Attackers often use fake names and domains to make malicious emails appear legitimate.
- SPF failures are strong indicators of a spoofed or unauthorized email and should always be investigated.
- Base64 encoding is frequently used to hide malicious content or embedded data.
- File extensions cannot be trusted—files may be disguised as PDFs but actually contain ZIP archives or other dangerous formats.
- Hex editors such as HxD are essential for identifying file types using hexadecimal signatures and magic numbers.
- Metadata analysis can reveal useful details about file authorship, timestamps, and potential attacker information.
- CyberChef is a powerful and flexible tool for decoding, analyzing, and transforming encoded or obfuscated data.

  

  
  
