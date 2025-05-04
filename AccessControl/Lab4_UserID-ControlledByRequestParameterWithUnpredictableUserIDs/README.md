# Access Control Lab 4: User ID controlled by request parameter, with unpredictable user IDs

***Port Swigger Accademy Lab***

After navigating to the lab's URL, I logged into `My Account` using the provided credential, `wiener:peter`.

After I logged into Wiener's account, I noticed Wiener's API-Key clearly visible.

![myAPI-Key](Images/AccessControlLab4_1_myAPI-Key.png)

Then, browsed around the blog searching for one of Carlos's posts. The below showed that I found a post that was posted by Carlos.

![carlosPost](Images/AccessControlLab4_2_carlosPost.png)

After that I clicked on Carlos's name on his post and saw that the `id=9` parameter can access another parameter. Since I use Burp to listen and intercept traffic, I needed to release the captured request by pressing `forward` on Burp.

![clickOnCarlosFromHisPost](Images/AccessControlLab4_3_clickOnCarlosFromHisPost.png)

The below screenshot was my attempt to keep a record of both Carlos's and Wiener's userID in one screen on Burp Repeater.

![CarlosID-andMine](Images/AccessControlLab4_4_CarlosID-andMine.png)

Take note of Carlos's userID on the Proxy Tab on Burp. Copy it. It will be useful later.

![takeNoteOfCarlosID](Images/AccessControlLab4_5_takeNoteOfCarlosID.png)

Next, I went back to Wiener account page, my account. I noticed that the URL parameter showed ID which was Wiener's userID.

![replaceWienerID-WithCarlos](Images/AccessControlLab4_8_replaceWienerID-WithCarlos.png)

Then, I replaced Wiener's ID with Carlos's and hit `forward`.

![replaceWienerID-WithCarlosOnBurp](Images/AccessControlLab4_9_replaceWienerID-WithCarlosOnBurp.png)

The result was I got access to Carlos's account and able to see Carlos's API-Key.

![getCarlosAPI-Key](Images/AccessControlLab4_10_getCarlosAPI-Key.png)

Copy Carlos's API-Key and submit it as shown in the below screenshot.

![submitCarlosAPI-Key](Images/AccessControlLab4_11_submitCarlosAPI-Key.png)

Now the lab was solved.

![labSolved](Images/AccessControlLab4_12_labSolved.png)

Here is a tiny tip. Keep a note along the way helped even though I took a lot of screenshots along the way.

![notes](Images/AccessControlLab4_13_notes.png)

## Mitigations Strategies
