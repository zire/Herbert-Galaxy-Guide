# Zero Inbox Workflow on Mac

## Outlook Rules & Shortcuts

Three local Exchange rules are needed. 

In Outlook menu, go to `Tools/Rules`. Under `Client Rules/Exchange`, create these:

![Client Exchange Rules](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/outlook-mac-00-rules.png)

Crete Rule-A to set up follow-up flag

![Rule A to follow up](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/outlook-mac-01-followup.png)

Create Rule-B to set up archive action

![Rule B to archive](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/outlook-mac-02-archive.png)

Create Rule-C to set up motion to move to local sent folder
![Rule C to sent](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/outlook-mac-03-sent.png)

Rule C is run automatically on the client. Rule B can use the same `^1` shortcut as the system default for Outlook for Mac. To set up shortcut for Rule A, do this:

Go to `System Preferences/Keyboard/Shortcuts/App Shortcuts`, click `+`. In `Application` tab, choose `Microsoft Outlook`. In `Menu Title`, type something that makes sense, for example, `To Follow Up`. In `Keyboard Shortcut`, pick a shortcut.

[Back to HitichHikder's Guide by Herbert](README.md)

