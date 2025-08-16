**File 2: `xss_stored.md`**

```markdown
# XSS Stored - DVWA

**Environment:**  
- Attacker: Kali Linux (192.168.20.11)  
- Victim: Debian (192.168.20.12)  
- DVWA Security Level: Low  

---

## Steps

1. On Kali, set a malicious payload in the input form of the DVWA XSS (Stored) module:
   ```html
   <script>alert('XSS Stored');</script>
````

2. Submit the form.

---

## Result

* On Debian, visiting the page triggers the payload automatically.
* The payload is permanently stored in the web application database.

**Observation:**

* Stored XSS executes automatically for anyone visiting the page.
* More dangerous than reflected XSS since it does not require further victim interaction.
* Can be exploited to steal credentials, escalate privileges, or hijack sessions.

```
