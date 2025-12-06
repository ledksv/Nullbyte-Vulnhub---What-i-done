NullByte — Write‑Up 

I began the assessment by identifying the target machine on the network and confirming that it was reachable. Once I had the correct address, I performed a full reconnaissance scan to map out the open services and understand the machine’s initial attack surface.

With the scan results in hand, I shifted to the web service running on the box. Visiting the site in a browser revealed a simple page, but closer inspection uncovered a hidden message embedded within one of the images. This hinted at additional paths to explore.

To expand the enumeration, I conducted directory discovery, which revealed further endpoints to investigate. Some of these didn’t immediately expose vulnerabilities, so I moved to a more controlled inspection using an intercepting proxy. By capturing the traffic and studying the application’s behavior, I identified an authentication point that appeared suitable for brute‑force analysis.

I used an external tool to perform a password‑guessing attack against this login. Once valid credentials were obtained, I logged into the next section of the application. This exposed a parameter vulnerable to SQL injection, which allowed me to extract additional sensitive information, including a hashed password. After cracking the hash, I was able to authenticate through SSH and gain access as a low‑privileged user.

From there, I carried out local enumeration to assess privilege‑escalation vectors. A misconfigured SUID binary provided the opportunity needed. By leveraging this weakness, I successfully elevated my privileges and gained full control of the machine.
