# Security Fundamentals Assessment

## 1. Objective

Perform a security assessment of an intentionally vulnerable OWASP Juice Shop application running locally in an authorized lab environment.

## 2. Scope

- **Target:** OWASP Juice Shop
- **URL:** `http://localhost:3000`
- **Environment:** Windows 10, Node.js v24.22.0
- **Tools:** Google Chrome Developer Tools, Network panel
- **Authorization:** Local training lab only

## 3. Methodology

1. Started the OWASP Juice Shop application locally.
2. Confirmed the application was accessible through the browser.
3. Inspected the main HTML document's HTTP response using Chrome Developer Tools.
4. Reviewed the response status and available security-related headers.
5. Inspected the application's configuration response.

## 4. Observation: Content Security Policy Header Not Observed

**Affected component:** Main HTML response (`/`)

**Observed result:** The main HTML response returned HTTP `200 OK`. The `Content-Security-Policy` header was not observed among the inspected response headers.

**Potential risk:** Without a Content Security Policy (CSP), browsers may have fewer restrictions on permitted resource sources. Depending on the application's other protections and client-side behavior, this can reduce defense-in-depth against certain injection attacks.

**Severity:** Preliminary informational / low-priority hardening recommendation. Exploitability and actual impact have not been demonstrated.

**Evidence:** `evidence/05-security-headers.png`

**Recommended mitigation:**

- Review the application's security requirements and resource dependencies.
- Design a restrictive CSP appropriate to the application.
- Test the policy in report-only mode before enforcing it.
- Verify that legitimate application functionality continues to work after deployment.

**Verification status:** The header was not observed in the inspected main HTML response. Further validation is required before treating this as a confirmed vulnerability.

## 5. Other Header Observations

The inspected response also included:

- `X-Content-Type-Options: nosniff`
- `X-Frame-Options: SAMEORIGIN`
- `Access-Control-Allow-Origin: *`

The wildcard CORS header requires endpoint-specific context before its security impact can be assessed. Its presence alone does not establish a vulnerability. The framing and content-type headers were observed as present.

## 6. Limitations

- Testing was limited to the local OWASP Juice Shop training environment.
- No exploit was demonstrated.
- No remediation was applied or verified.
- Findings are based on the observed responses and should not be generalized to other deployments.

## 7. Conclusion

The local training application was started successfully, and its HTTP response headers were inspected. The absence of an observed CSP header was recorded as a preliminary hardening recommendation. Further testing is needed to establish impact and confirm whether this should be reported as a vulnerability.

## 8. Evidence

The following screenshots were captured during the authorized local OWASP Juice Shop assessment:

1. `evidence/cmd.jpeg` — Command prompt showing the lab startup and environment.
2. `evidence/02-juice-shop-homepage.jpeg` — OWASP Juice Shop running locally.
3. `evidence/05-security-headers.jpeg` — Browser DevTools showing HTTP response headers.
4. `evidence/06-additional-response-headers...` — Additional response-header observations.

**Finding:** The Content Security Policy (CSP) header was not observed on the inspected main HTML response. Further validation is required before confirming a vulnerability.
