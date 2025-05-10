# Access Control Lab 4: User ID controlled by request parameter, with unpredictable user IDs

***Port Swigger Academy Lab***

After navigating to the lab's URL, I logged into `My Account` using the provided credential, `wiener: peter`.

After I logged into Wiener's account, I noticed Wiener's API key was clearly visible.

![myAPI-Key](Images/AccessControlLab4_1_myAPI-Key.png)

Then, I browsed around the blog, searching for one of Carlos's posts. The below shows that I found a post by Carlos.

![carlosPost](Images/AccessControlLab4_2_carlosPost.png)

After that, I clicked on Carlos's name in his post and saw that the `id=9` parameter could access another parameter. I could also access another ID post by changing the ID number. Since I use Burp to listen and intercept traffic, I needed to release the captured request by pressing `forward` on Burp.

![clickOnCarlosFromHisPost](Images/AccessControlLab4_3_clickOnCarlosFromHisPost.png)

The screenshot below was my attempt to keep a record of Carlos's and Wiener's userID in one screen on Burp Repeater.

![CarlosID-andMine](Images/AccessControlLab4_4_CarlosID-andMine.png)

Take note of Carlos's userID on the Proxy Tab on Burp. Copy it. It will be helpful later.

![takeNoteOfCarlosID](Images/AccessControlLab4_5_takeNoteOfCarlosID.png)

Next, I went back to the Wiener account page through `my account`. I noticed that the URL parameter showed ID, which was Wiener's userID.

![replaceWienerID-WithCarlos](Images/AccessControlLab4_8_replaceWienerID-WithCarlos.png)

Then, I replaced Wiener's ID with Carlos's and hit `forward`.

![replaceWienerID-WithCarlosOnBurp](Images/AccessControlLab4_9_replaceWienerID-WithCarlosOnBurp.png)

The result was I got access to Carlos's account and was able to see Carlos's API-Key.

![getCarlosAPI-Key](Images/AccessControlLab4_10_getCarlosAPI-Key.png)

Copy Carlos's API key and submit it as shown in the below screenshot.

![submitCarlosAPI-Key](Images/AccessControlLab4_11_submitCarlosAPI-Key.png)

Now the lab was solved.

![labSolved](Images/AccessControlLab4_12_labSolved.png)

Here is a tiny tip: Keeping a note along the way helped, even though I took a lot of screenshots along the way.

![notes](Images/AccessControlLab4_13_notes.png)

## Mitigations Strategies

+ Enforce Proper Access Controls (Authorization Checks)
  + Implement strict backend-side authorization checks to ensure users can only access their own resources, regardless of user ID in request parameters.
+ Avoid Using User-Controlled Identifiers in URLs
  + Don't rely on user-supplied IDs (like id=9) to control access. Instead, identify users via session tokens or securely stored user context.
+ Use Indirect Object References (IDOR Prevention)
  + Replace raw user IDs with opaque, securely mapped tokens (e.g., UUIDs or hashed values) that are hard to guess or reverse-engineer.
+ Implement Role-Based Access Control (RBAC)
  + Ensure each authenticated user is assigned a role, and access permissions are granted based on roles rather than user IDs.
+ Log and Monitor Access Attempts
  + Log abnormal access patterns, such as repeated ID enumeration, and alert on suspicious activity.
+ Use Rate Limiting and IP Throttling
  + Prevent automation of ID guessing by limiting the number of requests from a client or IP.
+ Security Testing (DAST/SAST)
  + Regularly test applications for IDOR vulnerabilities using automated tools and manual penetration testing.
  