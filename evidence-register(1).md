# Lab 3 — Evidence Register

| Evidence No. | Application | Test / Evidence | Evidence File Name | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **E-01** | Both | Benign marker SHA-256 hashes | E-01-benign-markers-SHA256 | Establish the identity and integrity of the benign markers. |
| **E-02** | DVWA | File-inclusion baseline | E-02-DVWA-File-inclusion-baseline | Show normal file/resource selection and identify the controlling parameter. |
| **E-03** | DVWA | LFI marker | E-03-DVWA-LFI-marker | Demonstrate successful local file inclusion using the benign marker. |
| **E-04** | DVWA | Path/error disclosure | E-04-Path-Error-Disclosure | Show path and application information disclosed through inclusion errors. |
| **E-05a** | DVWA | RFI server-side retrieval | E-05a-DVWA-RFI-server-side-retrieval | Demonstrate that DVWA made a server-side request to the controlled remote marker. |
| **E-05b** | DVWA | RFI response behaviour | E-05b-DVWA-RFI-response-behaviour | Demonstrate that the remote marker content was returned through the application. |
| **E-06** | Mutillidae II | LFI baseline | E-06-Mutillidae-LFI-Baseline | Establish normal file-inclusion behaviour. |
| **E-07a** | Mutillidae II | Marker preparation/copy | E-07a-Mutillidae-marker-copy | Document preparation of the benign marker for LFI testing. |
| **E-07** | Mutillidae II | LFI marker | E-07-Mutillidae-LFI-marker | Demonstrate successful local marker retrieval. |
| **E-08a** | Mutillidae II | RFI server-side retrieval | E-08a-Mutillidae-RFI-server-side | Demonstrate server-side HEAD and GET requests to the controlled marker service. |
| **E-08b** | Mutillidae II | RFI response | E-08b-Mutillidae-RFI-response | Demonstrate that the remote marker content was returned through Mutillidae. |
| **E-09** | DVWA | SQL injection baseline | E-09-DVWA-SQLi-baseline | Establish normal SQL-backed behaviour before injection testing. |
| **E-10** | DVWA | Boolean SQLi behaviour | No filename supplied | Demonstrate different application behaviour between true and false SQL conditions. |
| **E-11a** | Mutillidae II | Valid-account baseline | E-11a-Mutillidae-valid-test | Establish normal behaviour for an existing username with an incorrect password. |
| **E-11b** | Mutillidae II | Invalid-account baseline | E-11b-Mutillidae-invalid-test | Establish normal behaviour for a non-existent username. |
| **E-12** | Mutillidae II | SQLi authentication bypass | No filename supplied | Demonstrate authentication bypass through controlled SQL injection. |
