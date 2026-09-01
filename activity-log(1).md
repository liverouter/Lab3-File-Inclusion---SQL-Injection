# Lab 3 — Activity Log

| Step | Application | Activity / Action | Tool / Method | Result / Observation | Evidence |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | DVWA | Confirmed DVWA was running in Docker. | Docker / Browser | DVWA was available at `http://127.0.0.1:4280`. | — |
| **2** | Mutillidae II | Confirmed Mutillidae II was running in Docker. | Docker / Browser | Mutillidae II was available at `http://127.0.0.1:8888`. | — |
| **3** | Both | Created benign local and remote marker files for controlled file-inclusion testing. | Terminal | Markers were prepared for evidence-minimised testing. | E-01 |
| **4** | Both | Calculated SHA-256 hashes for the markers. | sha256sum | Local and remote marker hashes were recorded. | E-01 |
| **5** | DVWA | Established normal file-inclusion behaviour. | Browser | The page parameter was identified as controlling resource selection. | E-02 |
| **6** | DVWA | Tested LFI using the benign local marker. | Browser | The local marker content was successfully returned by the application. | E-03 |
| **7** | DVWA | Examined path and error disclosure. | Browser | PHP warnings disclosed the attempted path and application source locations. | E-04 |
| **8** | DVWA | Started the local HTTP marker service for RFI testing. | Python HTTP server | The marker service was made reachable from the Docker network. | E-05a |
| **9** | DVWA | Tested controlled RFI using the remote marker. | Browser / HTTP server | DVWA made a server-side request for the remote marker and the marker content was returned in the application response. | E-05a, E-05b |
| **10** | Mutillidae II | Established normal file-inclusion behaviour. | Browser | The file-inclusion functionality and controlling page parameter were identified. | E-06 |
| **11** | Mutillidae II | Prepared/copied the benign marker for LFI testing. | Terminal | Marker was made available for controlled testing. | E-07a |
| **12** | Mutillidae II | Tested LFI using the benign marker. | Browser | The local marker was successfully retrieved. | E-07 |
| **13** | Mutillidae II | Tested controlled RFI using the local HTTP marker service. | Browser / HTTP server | The Docker environment generated HEAD and GET requests for the remote marker. | E-08a |
| **14** | Mutillidae II | Verified the RFI response. | Browser | The remote marker content was displayed through Mutillidae. | E-08b |
| **15** | DVWA | Established the SQL injection baseline using a normal valid request. | Browser | `id=1` returned ID 1, first name admin and surname admin. | E-09 |
| **16** | DVWA | Completed the SQL baseline using an invalid input. | Browser | The invalid request did not return the normal record. | E-09 |
| **17** | DVWA | Performed a controlled boolean SQL injection comparison. | Browser | The true condition returned the record while the false condition returned no record. | — |
| **18** | Mutillidae II | Established normal authentication behaviour using an existing username and incorrect password. | Browser | `admin` / `admin` returned Password Incorrect. | E-11a |
| **19** | Mutillidae II | Established normal authentication behaviour using a non-existent username. | Browser | `test` / `test` returned Account does not exist for username: test. | E-11b |
| **20** | Mutillidae II | Performed a controlled SQL injection authentication test. | Browser | The input `' OR '1'='1' #` authenticated the session as the administrator account. | — |
| **21** | DVWA | Repeated the LFI test at the stronger Impossible security level. | Browser | `/tmp/local-marker.txt` returned File not found; the marker was not included. | — |
| **22** | Mutillidae II | Repeated the LFI test at Security Level 5 (Secure). | Browser | `/tmp/local-marker.txt` remained retrievable. | — |
| **23** | Both | Compared vulnerable and stronger security configurations. | Manual comparison | DVWA Impossible blocked the tested arbitrary file path, while Mutillidae Level 5 did not block the tested marker retrieval. | — |
| **24** | Both | Cleaned up the laboratory environment. | Terminal / Docker | Temporary marker service was stopped and temporary markers were removed. No database dump was created. | — |
