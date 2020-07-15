# Migrate Outlook Emails to Gmail

## Sort Outlook emails into monthly folder

In `Archive` local folder, select all emails, sort by `Date Received`. Select all the emails that were received during `YYYYMM`. 

In `Sent` local folder, do the same operation, sort by `Date Sent`. By now `YYYYMM` folder has all the emails that were received or sent out during YYYYMM. 

Select this `YYYYMM` local folder. In `Outlook/File`, select `Export`, select all the types, and start the export. This will export the entire local folder of your Outlook (not just the latst `YYYYMM` folder)  into one single massive `.olm` file with complete sub-folder structure. Depending on the size of your total local mails, this operation could take up considerable time. It's about 30~45 minutes for a single file of 16GB on my laptop. 

## Convert olm files into Apple Mail format

Buy this application, [OLM Converter Pro](https://www.olmconverterpro.com/). 

Open the olm file with OLM Converter Pro. Select only the `YYYYMM` folder. In `Convert To:` option, select `Apple Mail, Addressbook, Calendar`. Click `Start` to start the conversion. Choose the current path where the .olm file is saved on the next prompt window. This will turn the olm file into a folder that has one mbox file for each email sub-folder. 

![OLM Converter Pro](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/convert_olm.png)

## Set up Thunderbird and configure new local folders

Install Thunderbird add-on `ImportExportTools NG` by Christopher Leidigh. The latest version is 4.0.4 as of April 2020. Restart Thunderbird.

Right click to open the menu that shows `ImportExportTools`, select `Import mbox file` and `Import directly one or more mbox files`. In the dialog window for selecting file, select the mbox file in `TextEdit` format. 

A new folder under `Local Folders` in Thunderbird is created, named by default `mbox`. Change that to a more recognizable name, such as `YYYYMM`. 

## Sync up Gmail with local mbox files

Select `YYYMMM` folder in Thunderbird, select all the emails in this folder, right-click, select `move to` and point to the destination folder `XXX`. This will trigger the migration to move these local emails to the online folder labelled as `XXX` in your Gmail account. This is going to be take a while depending on the Internet connection.

When this process finishes, the local folder in Thunderbird shall be empty. All the emails originally in Outlook will now be available from your Gmail account under the label `XXX`. 

To make this process faster, it would be a good idea to turn off other labels for imap in gmail's settings. Thunderbird will by default try to download all the emails to the local drive from those labels flagged for imap. 

## Fix Connection Issue of Thunderbird

Thunderbird often generates an error message "connection to imap.gmail.com timed out" that could spoil an upload of thousands of emails after many hours. The issue seems to be caused more by Thunderbird than connection to Gmail per se. It requires almost the collection of all the below tricks to make this issue go away. 

1. Change Thunderbird's connection interval

	In Thunderbird, go to `Preferences/Advanced/Config Editor/` . Click `I accept the risk!`. Search for `mailnews.tcptimeout` and change its default setting from 10 to a large integer, like `1000` or `2000`. If this integer is too small, Thunderbird will give up attempt to connect to gmail very quickly. We need to tell Thunderbird to keep trying.
	
2. Use an app-specific password in Gmail for Thunderbird. Sometimes due to Thunderbird's security configuration (or, more like a bug), password entered from a Thunderbird client may not be easily recognized by Gmail server. An app-specific password will make that easier. To be able to see this option available in Google account setting, two-step authorization needs to be turned ON first according to [Google Help](https://support.google.com/accounts/answer/185833?hl=en). Go to [Security in Google Account Settings](https://myaccount.google.com/security), choose `App Passwords`.

3. Clean up cache in [Captcha](https://accounts.google.com/DisplayUnlockCaptcha) may help as well.

4. Use the strongest network connection to Gmail possible. If network connection to imap.gmail.com is weak, it'll be difficult to establish a handshake to Gmail server and complete an upload. Move laptop to an area where the wi-fi signal is the strongest, or connect laptop to LAN port on the router via a LAN cable.

5. Upload the small-sized emails first. It appears that, the bigger the uploaded email size, the more fragile the connection would be. It's advisible to sort emails by size in local Thunderbird folders and upload the smaller emails first. 

## Move Outlook Folder Files on Mac

Moving folder files in Outlook for Mac 2016.16.23 takes a bit of work. 

The message files are stored in this location:

`/Users/me/Library/Group Containers/UBF8T346G9.Office/Outlook/Outlook 15 Profiles/Main Profile/Data`

## Reference

[Stack Overflow: Where does Mac Outlook 2016 stores Mails (On my Mac)](https://superuser.com/questions/1152550/where-does-mac-outlook-2016-stores-mails-on-my-mac)

***

[Back to HitichHikder's Guide by Herbert](README.md)