sandbox escape PoC exploit available for VM2 library
A security researcher has released, yet another sandbox escape proof of concept (PoC) exploit that makes it possible to execute unsafe code on a host running the VM2 sandbox.

VM2 is a specialized JavaScript sandbox used by a broad range of software tools for running and testing untrusted code in an isolated environment, preventing the code from accessing the host's system resources or external data.

The library is commonly found in integrated development environments (IDEs), code editors, security tools, and various pen-testing frameworks. It counts several million downloads per month in the NPM package repository.

VM2 has had several critical sandbox escape disclosures over the past two weeks discovered by different security researchers, enabling attackers to run malicious code outside the constraints of the sandboxed environment.

The first sandbox escape flaw tracked as CVE-2023-29017 was discovered by Seongil Wi two weeks ago, with the latest two (CVE-2023-29199 and CVE-2023-30547) discovered by SeungHyun Lee.

Researchers from Oxeye discovered another sandbox escape tracked as CVE-2022-36067 in October 2022.

Sandbox escape flaw
The latest vulnerability is tracked as CVE-2023-30547 (CVSS score: 9.8 – critical) and is an exception sanitization flaw allowing an attacker to raise an unsanitized host exception inside "handleException()."

This function is meant to sanitize exceptions caught within the sandbox to prevent leaking information about the host. However, if an attacker sets up a custom "getPrototypeOf()" proxy handler that throws an unsanitized host exception, the "handleException" function will fail to sanitize it.

This helps the attacker "access the host Function," aka escape the sandbox restrictions and perform arbitrary code execution in the host context, allowing for potentially significant attacks.

The flaw was discovered by security analyst SeungHyun Lee of the Korea Advanced Institute of Science and Technology (KAIST), who found that it impacts all library versions from 3.9.16 and earlier.

The researcher has also published a proof of concept (PoC) exploit on his GitHub repository to demonstrate the feasibility of the attack, which creates a file named "pwned" on the host.
PoC released by the researcher (GitHub)
All users, package maintainers, and software developers whose projects incorporate the VM2 library are recommended to upgrade to version 3.9.17, which addresses the security flaw, as soon as possible.

Seongil Wi confirmed to BleepingComputer that the two bugs discovered by Lee are not related to the one he found.

Unfortunately, supply chain complexities affecting most open-source software projects might delay the upgrade of VM2 across the impacted tools. Coupled with the public availability of a PoC, many users may be left exposed to risks for an extended duration.
