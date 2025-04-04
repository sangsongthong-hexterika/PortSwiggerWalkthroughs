# Lab: File Path Traversal Simple Case

I started by reading through the content of the lab on PortSwigger's Web Security Academy and navigating to the lab URL.

File Path Traversal is one of the easiest attack vectors to identify in web application penetration testing. The core idea is that an insecure website allows unauthorized users to access sensitive system data that should be restricted.

The basic method to test for this vulnerability is simple: manually entering `../../../etc/passwd` often does the trick. The `../../../` instructs the Linux server to move up three directories to reach the root (`/`). On a Windows server, `\` is typically used instead.

After reaching `/`, the `/etc/passwd` path directs the server to the `/etc` directory, retrieves the passwd file, and displays its content.

## Identifying the Correct Injection Point

However, you can’t just add `../../../etc/passwd` anywhere on a website and expect it to work. It only works when injected into a request that interacts with files.

Previously, I understood how path traversal works but didn’t know where to apply it. Now, I understand that it needs to be inserted into a request that references a file.

On the lab website, I first tried appending it to the URL directly, but it didn’t work. Then, I navigated to a displayed item and inserted it into the URL, but that also failed.

At first glance, it seemed logical to inject `../../../etc/` passwd where an item was displayed, but this was incorrect.

![incorrectPlaceToCheck](Images/PortSwiggerFileTransversal-1.png)

The correct injection point was found by right-clicking on an image and selecting "Open image in a new tab." The red box in the screenshot highlights the filename in the URL. Once you see a filename, that is the place to check for **Path Traversal**.

![correctPlaceToCheck](Images/PortSwiggerFileTransversal-2.png)

## Exploiting the Vulnerability

To make this work, I used Burp Suite to capture the HTTP request. The screenshot below shows the original request before modification, with the key part of the request highlighted.

In older CTFs like TryHackMe and HackTheBox, path traversal payloads were sometimes tested directly in the browser’s address bar. However, modern web browsers have stricter security measures that prevent this. Instead, you can modify the request using Burp Suite

![unmodifiedRequestInBurp](Images/PortSwiggerFileTransversal-3.png)

After modifying the request in Burp Suite, I sent it using the Repeater tool. I prefer using Repeater because if I make a mistake, I can easily resend the request without capturing new traffic.

![success](Images/PortSwiggerFileTransversal-4.png)

As you can see, I was able to make the system reveals the content inside `/etc/passwd` which contains user account information such as usernames, user IDs, and home directories.

The /etc/passwd file contains user account information, such as usernames, user IDs, and home directories. However, it does not store passwords. In modern Linux systems, password hashes are stored separately in /etc/shadow, which requires higher privileges to access.

## Mitigation

Coming soon!

**Reference:** [Port Swigger File Path Traversal](https://portswigger.net/web-security/file-path-traversal)
