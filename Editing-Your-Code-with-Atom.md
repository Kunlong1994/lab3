If you prefer modern text editors, you can use the [Atom Editor](https://atom.io) to edit the code on your Raspberry Pi. Atom is a powerful text editor with all kinds of great features built in. Additionally, you can extend Atom's capabilities by installing "packages," or small pieces of software that enable new features.

To edit the code on your Raspberry Pi from your laptop you will need to install Atom on your laptop. Get the version that is right for your Operating System (Mac, Windows, Linux).

Once downloaded and installed we will then install/add the package called `ftp-remote-edit`. To install this, go to `Preferences`. Then in the left pane, click `Install`.

Search for `ftp-remote-edit` and choose `install`

After the package is installed, go to `Packages` in the top bar and choose `Ftp-Remote` -> `Edit Servers`.

Give your session a password (this can be anything, I will do `raspberry`), then hit `Enter`

The first time you setup a remote editing session, you will need to specify your server. If you can see your Raspberry Pi on the local network and `ping` it using something like `ping ixe00.local` (remember `00` is your numbers as written on the SD Card) then you can use the foll0woing settings:

The name of the server: `ixe[00]` (where 00 are your numbers)

The hostname of IP address of the server: `ixe[00]`

Port: `22`

Username for authentication: `pi`

`Check` use sftp (ssh) connection

Initial Directory: `\home\pi`

Save this information. You will then go back to the main editor window. From here, you can get access to the files on your pi by showing the server connection file menu.

Choose `Packages` -> `Ftp-Remote` -> `Toggle  ^Space` (you could also use the `^Space` hotkey`)

This will open a pane on the right side of the editor showing a file browser with you Pi. Click the top level of the browser (where it says `ixe[00]`) to show the files.

You should then see the file tree. Navigate to the directory and file you would like to edit. Then click the file to open it in the Atom editor. You should see the code in the editor and should be able to make your changes.

When you are done, save the file. This will save the file on your Raspberry Pi. You should see a green pop-up in the upper right saying the file was saved successfully.

Note: you are editing the file on your Pi, not on your local machine. All the changes will be made to the Pi.

When you are done and have saved your file, you should be able to close it and the Atom editor.

The next time you want to edit files on your Pi, make sure the Pi is connected to the network. Then you can go to `Packages` -> `Ftp-Remote` -> `Toggle  ^Space` or hit `^Space` to get back to your file browser on the right side of the editor. 

