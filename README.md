This is a fork of the [original Drupebox](https://github.com/duncanhawthorne/drupebox) script, by [Duncan Hawthorne](https://github.com/duncanhawthorne).
It addresses ownership and permissions issues that occur if your sync folder contains multiple files with different ownerships and permissions. It preserves the users, groups and permissions of your existing files and makes reasonable assumptions about new files being downloaded from Dropbox.
if all your files that you keep in sync have the same owner, you don't need this.

# Drupebox
Drupebox is a Dropbox sync app built for the Raspberry Pi.

![](https://github.com/mihaimiculescu/drupebox_fork/blob/master/icon.png)

Drupebox enables Dropbox syncing on a Raspberry Pi using the Dropbox API, supporting uploading, downloading, and syncing a folder on your computer with an App folder inside Dropbox.

Drupebox is a python script which you run from the Raspberry Pi OS terminal. Drupebox can be run regularly (e.g. hourly or on each boot), to keep your folder regularly in sync.

How to use
-----------
**1. New users**

Install dependencies for Drupebox
```
sudo apt install git python3-configobj python3-send2trash python3-dropbox
```

Download Drupebox into the Drupebox script folder
```
git clone https://github.com/mihaimiculescu/drupebox_fork.git drupebox
```

Run Drupebox
```
sudo python3 drupebox/drupebox.py
```

Authorise Drupbox to sync your Dropbox folder
* Drupebox will start an authorization process with Dropbox.
* Click the link to Dropbox that will appear in the terminal (or visit that link using a different computer).
* Log into Dropbox and approve the authorization for the app. The app will only have authorization to a single App folder in Dropbox - the newly created "Drupebox" folder within the Apps folder. Drupebox will have no access to the rest of your Dropbox.
* Dropbox will give you a code to paste back into the terminal window to complete the authorization. This code will not leave your Raspberry Pi.
* Tell Drupebox the folder on your computer to keep in sync with Dropbox, or press enter to select the default folder /home/pi/Dropbox/.
* Your selected folder on your Raspberry Pi will then sync with the Drupebox folder.

Keep your folder in sync
* When Drupebox is first run, Drupebox will do an upload of the files in the folder on your Raspberry Pi to the newly created Drupebox folder in your Dropbox.
* When you run Drupebox again, it will download/upload the local/remote additions/changes/deletions to keep the folder on your Raspberry Pi and the Drupebox folder in Dropbox in sync. Files will be synced only where changes have been made.
* The Drupebox script can be run from a cron job to keep your folder constantly in sync.

**2. Existing users migrating from original Drupebox script**
* Copy `drupebox.py` and `libs_drupe.py` from this repo into your local `drupebox` folder, overwriting the existing ones.
* Run these commands:
```
sudo chown root:root /dev/shm/*
cd ~
```
* Run `sudo python3 drupebox/drupebox.py`. It will take you again through the authorisation process, as described above. <br>
Make sure to provide the **same** sync folder as you did originally, providing the **full** path, with ending slash **/**. <br>
Example: if your sync folder is `/home/<your_user_name>/Dropbox/` type it as such.
* If you run Drupebox from a cron job, remember to update it by prefixing with `sudo` the relevant line.

Drupebox also supports other linux environments whose distros support sudo.

*A raspberry is an aggregate fruit composed of small individual elements called drupes which together form the botanic berry.
