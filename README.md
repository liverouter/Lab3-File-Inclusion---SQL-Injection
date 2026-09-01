# Lab 3 — File Inclusion & SQL Injection Assessment

## Overview

This laboratory assessment focused on the practical identification and validation of **Local File Inclusion (LFI)**, **Remote File Inclusion (RFI)**, and **SQL Injection (SQLi)** vulnerabilities within an isolated web-security training environment.

Testing was performed against:

* **DVWA (Damn Vulnerable Web Application)**
* **OWASP Mutillidae II**

All testing was conducted within the authorised laboratory scope using benign markers and controlled requests.

---

## Objectives

The objectives of the assessment were to:

* Establish normal application behaviour before testing.
* Identify and validate Local File Inclusion (LFI).
* Identify and validate Remote File Inclusion (RFI).
* Demonstrate server-side retrieval of a controlled remote resource.
* Identify and validate SQL injection through controlled behavioural testing.
* Compare vulnerable and stronger security configurations.
* Record reproducible evidence for each activity.
* Clean up the laboratory environment after testing.

---

## Lab Environment

| Component                 | Details                  |
| ------------------------- | ------------------------ |
| Attacker / Testing System | Kali Linux               |
| DVWA                      | Docker container         |
| Mutillidae II             | Docker container         |
| DVWA URL                  | `http://127.0.0.1:4280`  |
| Mutillidae II URL         | `http://127.0.0.1:8888`  |
| Remote Marker Service     | Python HTTP server       |
| Marker Service Port       | `8000`                   |
| Testing Network           | Local Docker environment |

The remote marker service was bound to `0.0.0.0` so that the Docker containers could reach the host-side HTTP service through the relevant Docker network.

---

## Testing Approach

Testing followed a controlled progression:

1. Establish the application baseline.
2. Prepare benign markers.
3. Verify marker integrity using SHA-256.
4. Test LFI using the local marker.
5. Test RFI using the controlled remote marker.
6. Record server-side and browser-side evidence.
7. Establish SQL injection baselines.
8. Perform controlled SQL injection tests.
9. Repeat relevant tests at stronger security levels.
10. Document observations and security controls.
11. Clean up the environment.

No sensitive system files were intentionally retrieved.

---

## File Inclusion Testing

### DVWA

The DVWA file-inclusion functionality was tested using the `page` parameter.

The local marker was successfully included, demonstrating LFI.

A controlled HTTP server was then used to host the remote marker. DVWA generated a request to the marker service and the marker content was returned through the application, demonstrating RFI.

The RFI server recorded the request, providing server-side evidence of remote retrieval.

### Mutillidae II

Mutillidae II was tested using its file-inclusion functionality.

The benign local marker was successfully retrieved, demonstrating LFI.

The same controlled remote marker was subsequently used for RFI testing. The marker server recorded `HEAD` and `GET` requests originating from the Mutillidae Docker environment, and the marker content was displayed through the application.

---

## SQL Injection Testing

### DVWA

A normal SQL-backed request was first established using:

```text
id=1
```

The application returned the administrator record.

A controlled boolean comparison was then performed:

```text
1' AND '1'='1
```

The true condition returned the record.

The corresponding false condition:

```text
1' AND '1'='2
```

returned no record.

The difference in behaviour demonstrated that the supplied input affected SQL query logic rather than simply generating an error.

### Mutillidae II

Normal authentication behaviour was established first.

An existing username with an incorrect password returned a password error, while a non-existent username produced an account-not-found response.

A controlled SQL injection test using:

```text
' OR '1'='1' #
```

resulted in authentication as the administrator account.

This demonstrated that user-controlled input could alter the authentication query logic.

The initial input that produced an application exception was not treated as vulnerability proof.

---

## Security-Level Comparison

### DVWA

At the stronger **Impossible** security level, the tested local marker path:

```text
/tmp/local-marker.txt
```

returned:

```text
File not found
```

The tested arbitrary file inclusion was therefore prevented.

### Mutillidae II

At **Security Level 5 (Secure)**, the tested local marker remained retrievable.

This indicated that the selected Mutillidae security configuration did not prevent the specific file-inclusion behaviour tested during this assessment.

---

## Evidence

Evidence was captured using the following naming convention:

```text
E-01-benign-markers-SHA256
E-02-DVWA-File-inclusion-baseline
E-03-DVWA-LFI-marker
E-04-Path-Error-Disclosure
E-05a-DVWA-RFI-server-side-retrieval
E-05b-DVWA-RFI-response-behaviour
E-06-Mutillidae-LFI-Baseline
E-07a-Mutillidae-marker-copy
E-07-Mutillidae-LFI-marker
E-08a-Mutillidae-RFI-server-side
E-08b-Mutillidae-RFI-response
E-09-DVWA-SQLi-baseline
E-11a-Mutillidae-valid-test
E-11b-Mutillidae-invalid-test
```

The complete evidence descriptions are maintained in:

* [`evidence-register.md`](evidence-register.md)

The chronological record of activities is maintained in:

* [`activity-log.md`](activity-log.md)

---

## Marker Integrity

### Remote Marker

SHA-256:

```text
117ba05a69fa42c87a177577f81f21a67d7367f2371f3e4aaf311e24043b219d
```

The marker was intentionally benign and contained only test text.

---

## Scope and Safety

The assessment was performed only against the authorised laboratory applications.

The following limitations were observed:

* Benign markers were used for file-inclusion validation.
* No sensitive files were intentionally targeted.
* No database dump was performed.
* No credential harvesting was performed.
* No private keys or operating-system secrets were collected.
* Testing stopped after sufficient evidence was obtained.
* The temporary HTTP marker service was used only for controlled RFI validation.

---

## Cleanup

After testing:

* Temporary marker files were removed.
* The temporary HTTP marker server was stopped.
* The laboratory applications were returned to their intended state.
* No persistent testing services were left running.
* No unnecessary extracted data was retained.

---

## Conclusion

The assessment successfully demonstrated practical exploitation and validation of LFI, RFI and SQL injection within an isolated training environment.

The comparison between security configurations also demonstrated that security controls can significantly change application behaviour. DVWA's Impossible configuration prevented the tested arbitrary file inclusion, while the tested Mutillidae Security Level 5 configuration continued to permit retrieval of the benign local marker.

The assessment was completed within scope using controlled, evidence-minimised testing.
