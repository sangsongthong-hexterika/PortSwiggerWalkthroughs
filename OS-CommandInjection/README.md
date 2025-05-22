# Lab: OS Command Injection, Simple Case

**Lab:** Port Swigger Academy

Navigate to the lab URL. Note that the URL with the `productID=number` was not the correct one. Do not confuse it with the other attack vector. I put the first two screenshots here with this explanation so you won't get lost in it.

The below screenshot is the orginal of the incorrect attack vector.

![originalProductID](images/OS-CommandInjection_1_originalProductID.png)

The below screenshot is the previous screenshot after trying to add `| whoami &" and found that it didn't work.

![addWhoAmI](images/OS-CommandInjection_2_addWhoAmI.png)

On the product discription page, scroll down to see the choosing the store section. Pick one of them and click "Check Stock".

![checkStock](images/OS-CommandInjection_3_checkStock.png)

Capture the request on Burp. Take a look at the screenshot below, the box areas highlight the spot to test the OS-Command Injection.

You can see that the URL has to show something like `/product/stock` rather than `/product/stock=1`. If the URL uses `/product/stock=1`, then it can be a different type of attack.

In OS-Command Injection, the command is at the end of the captured request. This is where I want to spend time climbing.

![checkStockOriginalBurp](images/OS-CommandInjection_3_checkStockOriginalBurp.png)

Capture the request on Burp and make changes in the `storeID`'s value by adding `|whoami &` at the end to trick the server to show the result of the `whoami` command. If the server displays the result on the web page, it means the server was vulnerable to OS-Command Injection attack.

Before moving on, it is worth noting that the OS-Command Injection URL ended with `/product/stock` without showing something like `id=something`. This makes it different than the attack that users can modify the URL.

Another point to mention is the vulnerable code is written at the end of the source code as `storeID=number` and the `number` is the only thing that changes once I click on another product, but the change will not show on the URL form.

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
