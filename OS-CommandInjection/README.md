# Lab: OS Command Injection, Simple Case

**Lab:** Port Swigger Academy

![originalProductID](images/OS-CommandInjection_1_originalProductID.png)

![addWhoAmI](images/OS-CommandInjection_2_addWhoAmI.png)

![checkStock](images/OS-CommandInjection_3_checkStock.png)

![checkStockOriginalBurp](images/OS-CommandInjection_3_checkStockOriginalBurp.png)

![checkStockAddWhoAmI](images/OS-CommandInjection_4_checkStockAddWhoAmI.png)

I have successfully tricked the server to reveal the result of running `whoami` command.

Getting this result is very important because it is a Proof of Concept (PoC) that this system has OS-Command Injection Vulnerability.

It also tell which user was the one running this page which can serve as the starting points for privilege escalation.

![whoAmIResult](images/OS-CommandInjection_5_whoAmIResult.png)

The screenshot below showed that I have successfully completed this lab.

![labSolved](images/OS-CommandInjection_6_labSolved.png)

The last two screenshots below were just me testing the page using the command `echo` to make it showed something that does not belong to the web server out of my own curiosity.

This one was the command I ran on Burp.

![playAround](images/OS-CommandInjection_zz_playAround.png)

This one was the result of running the command in the previous screenshot.

![playAroundResult](images/OS-CommandInjection_zz_playAroundResult.png)

---

**Author:** Sangsongthong C.
**Publish Date:**
