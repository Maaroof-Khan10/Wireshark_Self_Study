# Used: 2015-02-08 - Traffic Analysis Exercise: Mike's Computer is "Acting Weird"

## First Steps

-   **Date and time of the activity:** 2015-02-08, between 18:31 (Found from the Time column).
-   **IP address of Mike's desktop computer:** `172.16.137.40` (Found by filtering `nbns`).
-   **Hostname of Mike's desktop computer:** `MIKE-PC` (Found by filtering `nbns`).
-   **MAC address of Mike's desktop computer:** `08:00:2b:ef:ab:7c` (Found by using `Packet Details -> Ethernet II`).

## Analysis

Mike visited `harveyouellet.com` and `cwvancouver.com` (seen in the DNS traffic at 18:31).

A file, `arrowu.jpg`, was downloaded. After checking its MD5 hash on VirusTotal, it was found to be malicious.

## Conclusion

The root cause was the `arrowu.jpg` image that contained a malicious malware in it. Mike probably opened a wrong email.