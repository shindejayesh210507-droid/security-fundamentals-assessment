# Security Fundamentals Assessment — OWASP Juice Shop

## Lab Environment
- Target: OWASP Juice Shop
- Environment: Authorized local training lab
- Target URL: `http://localhost:3000`
- Assessment scope: Intentionally vulnerable application running locally

## Finding 1 — DOM-Based Cross-Site Scripting (DOM XSS)

### Affected Component
OWASP Juice Shop search functionality / client-side DOM handling.

### Risk
User-controlled search input can be interpreted as executable JavaScript in the browser. In a real application, DOM XSS can allow malicious scripts to execute in a victim's browser under the application's origin, potentially enabling actions such as reading accessible page data or performing actions as the victim.

### Evidence
The Juice Shop DOM XSS challenge was successfully triggered using the lab's documented challenge payload:

```html
<iframe src="javascript:alert('xss')">
```

The application displayed the XSS alert and reported that the **DOM XSS** challenge was successfully solved.

### Recommended Mitigation
- Treat all client-side input as untrusted.
- Avoid inserting untrusted data into dangerous DOM sinks such as `innerHTML`.
- Prefer safe DOM APIs such as `textContent` where applicable.
- Apply context-appropriate output encoding.
- Sanitize HTML when HTML input is genuinely required.
- Use a strong Content Security Policy (CSP) as defense in depth.

### Severity / Impact
High impact potential depending on application context, authentication state, and accessible data. The lab demonstrates the vulnerability intentionally; production severity should be determined from the application's actual attack surface.

## Evidence Checklist
- [x] Local authorized lab used
- [x] DOM XSS challenge successfully solved
- [x] Screenshot of successful challenge saved by the assessor
- [ ] Add the screenshot to this repository as `evidence/dom-xss-success.png`

## Scope Statement
Testing was performed only against the intentionally vulnerable OWASP Juice Shop instance running in the authorized local lab environment. No unauthorized systems were tested.
