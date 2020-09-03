**_What we want is to be able to update the main repository and have the students pull in the changes to their local machines and work with the templates we provide for each lab. They then need to push their final codes/videos and everything which needs to be submitted for the lab to their forked repo ( forked from the main repo to their git account)._**

1) We first have to fork/create a copy from the main repository to our local github account:-
  * Go to https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices
  * Click on **fork** , this will create a copy of the main repository on your github account.

2) We then create a clone of the main repository on our local machine :- 
  * Open terminal on your local machine and navigate to the folder where you want to work.
  * Write **"git clone https://github.com/FAR-Lab/Developing-and-Designing-Interactive-Devices"**

3) Work on your local machine by changing/adding files to the particular lab folder accordingly.

4) To pull in new data/new lab (in your local machine repo) from the main repo, write **"git pull"** in the terminal.

5) To push your final lab data to your local repo ( on github ), follow these instructions:
  * write "git status" on terminal. This will give you a list of files changed and added by you on your local machine.
  * To add these files to your local repo, use **" git add < filename >"** or **"git add ."** ( to add all changes/files).
  * To commit these changes, use **"git commit -m < write a message >** . This message will describe what you are pushing/submitting.
  * To push these changes to your local git repo use, **"git push < your local repo link >"**