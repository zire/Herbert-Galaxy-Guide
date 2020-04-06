# Fix Time Machine Backup Issue on NAS


## The Issue

Sometimes Time Machine's automatic backup on home NAS doesn't work. The error message says `Time Machine could not delete the backup disk image ".....sparsebundle"`.

![issue](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_01_issue.png)

Not even Stack Overflow provides much help on this. My fix is to delete the corrupted shared folder on NAS and configure this Time Machine backup anew. It's a bit of annoyance but can be done in five minutes following the below guide.


## Fix

1. Delete the current destination shared folder on NAS

	![delete](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_02_delete_shared_folder.png)

2. Confirm the deletion. Deleting a shared folder on NAS is a big deal. A double confirmation is necessary. 

	![confirm deletion](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_03_confirm_deletion.png)

3. Create a new shared folder on NAS for backup through Time Machine. No need to use checksum, which slows down backup process considerably. No need to apply encryption since this is a local-to-local backup.

	![create new shared folder](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_04_create_new_shared_folder.png)
	
4. Confirm the settings before creating the folder

	![confirm settings](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_05_confirm_settings.png)
	
5. This fix doesn't involve any changes to the NAS user created for Time Machine - `timemachineuser` as it's on my NAS. When the old backup shared folder is deleted, the link between the Time Machine user and the backup folder is gone. So we need to re-establish that access. 

	![access to TM user](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_06_access_for_TM_user.png)

6. The last step is to make sure NAS has the appropriate file sharing protocol. `AFP` has served me well. `SMB` doesn't seem to jive with a few other configurations sometimes.

	![fie sharing](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_07_file_sharing_option.png)
	
We should be ready to run Time Machine backup again with this new setup.

## Configuration

1. I've tried different ways to connect to NAS for the purpose of Time Machine backup. It's not as obvious or straightforward as one would think, and little documentation can be found anywhere. The below works for me:
	
	![connect to shared folder](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_08_connect_to_network_folder.png)

2. When prompted for mounting the shared folder, choose the folder that was just created

	![mount](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_09_mount_backup_folder.png)
	
3. Open Time Machine on mac, delete the original backup folder (which was just deleted) from Time Machine's preferences and point Time Machine to the newly created backup folder.

	![select](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_10_select_new_folder.png)
	
4. With that, you're ready to run Time Machine backup again on the new backup shared folder on NAS. 

	![ready](https://galaxy-guide.s3-ap-northeast-1.amazonaws.com/time_capsule_11_ready_to_go.png)

***

[Back to HitichHikder's Guide by Herbert](README.md)