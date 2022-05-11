## Leaky Forms: A Study of Email and Password Exfiltration Before Form Submission (USENIX Security'22)

This repository contains the code for our [USENIX Security'22](https://www.usenix.org/conference/usenixsecurity22) paper titled
_Leaky Forms: A Study of Email and Password Exfiltration Before Form Submission_.

The paper is based on a measurement of email and password collection that occurs before the form submission on the top 100,000 websites. We evaluate the effect of user location (EU vs. US), browser configuration (desktop vs. mobile), and interaction with consent dialogs (accept all/reject all/no interaction).

For a more detailed overview and access to our data, please visit the [project's homepage](https://github.com/leaky-forms).

### Crawler

**Code**: https://github.com/asumansenol/leaky-forms-crawler

A high-level overview of our crawler is given below:
![Crawler Arch](https://user-images.githubusercontent.com/48864422/156778150-9915495d-21e3-436f-ab9f-0a639a15701c.png)

We extended DuckDuckGo’s **[Tracker Radar Collector](https://github.com/duckduckgo/tracker-radar-collector)** to measure email and password exfiltration. Our crawler was capable of detecting and filling email and password fields, and intercepting script access to filled input fields.

**Email field detection**: In order to identify email fields, we integrated into our crawler [Firefox Relay](http://mozilla.github.io/fathom/)’s [Fathom](http://mozilla.github.io/fathom/)-based [email field classifier](https://github.com/mozilla/fx-private-relay/blob/v1.2.2/extension/js/email_detector.js). Using this model allowed us to identify 76% more email fields than we would detect by simply searching for input fields with type `email`.

**Consent automation**: We integrated [Consent-O-Matic](https://github.com/cavi-au/Consent-O-Matic/) into our crawler to investigate the effect of users’ consent preferences. Consent-O-Matic ([Nouwens et al.](https://arxiv.org/pdf/2001.02479.pdf)) is a browser extension that can recognize and interact (e.g., accept or reject cookies) with various Consent Management Provider (CMP) pop-ups. We configured Consent-O-Matic to log detected CMPs, and interact with the CMP.

### Leak Detector

**Code**: https://github.com/asumansenol/leaky-forms/tree/main/leak-detector

Leak detector module searches for the filled email address and the password, and their various encodings and hashes in the HTTP traffic. The module is based on [Englehardt et al.’s method](https://petsymposium.org/2018/files/papers/issue1/paper42-2018-1-source.pdf), but it was improved to detect novel ways to exfiltrate the personal data. 

### Analysis

**Code**: https://github.com/asumansenol/leaky-forms/tree/main/analysis

You can find the Jupyter notebooks, pickles and CSVs that are used in the [analysis folder](https://github.com/asumansenol/leaky-forms/tree/main/analysis).

### Reference

```tex
@article{
    author    = {Asuman Senol and Gunes Acar and Mathias Humbert and Frederik Zuiderveen Borgesius},
    title     = {{Leaky Forms: A Study of Email and Password Exfiltration Before Form Submission}},
    booktitle = {Proceedings of the 31st USENIX Security Symposium (USENIX)},
    year      = 2022,
    month     = August
}
```
