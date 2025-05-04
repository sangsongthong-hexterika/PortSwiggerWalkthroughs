# Lab 3: User Role Controlled By Request Parameter

***Port Swigger Academy Lab***

After navigating to the lab's URL, I logged into the login panel using the given credential: `wiener: peter`, as shown in the screenshot below.

![LoginWithAGivenNormalUserCredential](Images/AccessControlLab4_1_LoginWithAGivenNormalUserCredential.png)

The screenshot below shows a successful attempt to log into the provided account using the username `wiener`. One thing to notice is that at this point, the URL parameter has `id=wiener` appended at the end.

![LoginAsNormalUser](Images/AccessControlLab4_4_LoginAsNormalUser.png)

I believe this part served as good learning for a beginner, so I included it. It is to be noted that this lab was about **User role controlled by request parameter**. This hinted that we need to modify something related to the *request parameter*.

![ChangedParameterID-toAdmin](Images/AccessControlLab4_5_ChangedParameterID-toAdmin.png)

I captured this request with Burp Suite as shown below.
As you can see, the admin's cookie was **admin=false**.
![CaptureTheTrafficAfterChangedParameterID-toAdminOnBurpAdminIsFalse](Images/AccessControlLab4_6_CaptureTheTrafficAfterChangedParameterID-toAdminOnBurpAdminIsFalse.png)

I tried changing the ***admin=false*** into ***admin=true*** before sending it. It seemed the server refused to let me log in as admin, so I had to move to another page to perform this attack.

![onBurpProxyAdminIsTrue](Images/AccessControlLab4_7_onBurpProxyAdminIsTrue.png)

Still logging in as the user wiener, I navigated to the `/admin` page. Upon catching the traffic with Burp, there is a cookie called ***Admin=false***. It is noted that without logging in as `wiener`, I wouldn't see the cookie: ***Admin=false*** in the first place. Another point to note was that this time, I attacked the `/admin` page instead of trying to manipulate `id=wiener` into `id=admin`. Believe me, I did that, but it did not lead me to solve this lab and will cause further confusion, so I did not include them here.

![navigateToAdminPage](Images/AccessControlLab4_8_navigateToAdminPage.png)

Now, I changed `Admin=false` to `Admin=true` on the `/admin` page before hitting the ***send*** button on Burp.

![changeAdminToTrue](Images/AccessControlLab4_9_changeAdminToTrue.png)

As you can see in the screenshot below, I was able to access the admin page and see other users. Next, I clicked delete, Carlos. Don't forget to capture the traffic through Burp. We still need to use Burp.

![onAdminPage](Images/AccessControlLab4_10_onAdminPage.png)

Take a look at the screenshot below. You can see that while I was trying to delete user ***Carlos***, I still needed to be an admin to do it. I still got the ***Admin=false*** in the request. If I sent the request right away without changing its value, I would not be able to delete ***Carlos***.

![AttemptToDeleteCarlosOnBurpAdminIsFalse](Images/AccessControlLab4_11_AttemptToDeleteCarlosOnBurpAdminIsFalse.png)

Upon capturing the request, I had to change the ***Admin=false*** to ***Admin=true*** again in order to delete the user ***Carlos***. The reason that we had to do this again was that we needed to have permission to do so - by performing the attack as an administrator. This is why this attack is dangerous -- because an attacker, me, can trick the server to allow me to login as an administrator so I could perform a dangerous action.

![AttemptToDeleteCarlosOnBurpChangeAdminToTrue](Images/AccessControlLab4_12_AttemptToDeleteCarlosOnBurpChangeAdminToTrue.png)

As you can see, this lab is solved.

![LabSolved](Images/AccessControlLab4_13_LabSolved.png)

## Mitigations Strategies
