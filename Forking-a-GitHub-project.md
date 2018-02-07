## Why?
If you fork a project you create a linked copy of that original project in your own GitHub account. After that, you can easily make your own changes without submitting any changes to the original source. 
This is how we would like you to submit your code parts of the homework.
## How?
It's super simple. Go to the webpage of the GitHub project you'd like to fork e.g. the [simple-ChatBot](https://github.com/FAR-Lab/simple-ChatBot). Click on the fork button on the top right of the page. GitHub will go ahead and create a personal copy of this repository. You can find this fork now under your own personal projects. If you want to download (clone) it just uses the link to your personal copy. 

So given this Example you would **NOT** type 

<img src="https://grassrootsy.files.wordpress.com/2010/07/dont.png" width="25"> ` git clone https://github.com/FAR-Lab/simple-ChatBot` <img src="https://grassrootsy.files.wordpress.com/2010/07/dont.png" width="25"> 
  
**BUT**

<img src="http://www.clker.com/cliparts/9/I/e/1/i/B/dark-green-check-mark.svg" width="25"> `git clone https://github.com/**_YourGITRepoName_**/simple-ChatBot` <img src="http://www.clker.com/cliparts/9/I/e/1/i/B/dark-green-check-mark.svg" width="25">

## What if - I already cloned the original source?
In this case, the origin of the project needs to be changed. 
First follow the above steps to create a forked version on your GitHub account. Copy the link to the fork version. 

Second, go to the terminal and navigate to the project folder(e.g.```~/simpleChatBot```) and verify that indeed the project is cloned from the original source. Type ```git remote -v```  to see what the 'origin' is. It likely will say something like:
```
origin	https://github.com/FAR-Lab/simple-ChatBot (fetch)
origin	https://github.com/FAR-Lab/simple-ChatBot (push)
```
This origin needs to be changed so that the changes you made are committed and pushed to your personal forked copy. 
This is done by typing
```
git remote set-url origin https://github.com/**_YourUserName_**/simple-ChatBot
```
Verify that this change worked by again typing ```git remote -v```. It should say

```
origin	https://github.com/**_YourUserName_**/simple-ChatBot (fetch)
origin	https://github.com/**_YourUserName_**/simple-ChatBot (push)
```

Now the changes that were made to the project can be submitted to the new origin. 
```
git add .
git commit -m "Some short comment about what was changed."
git push
```
For more information also have a look at the [GitCheatSheet](https://education.github.com/git-cheat-sheet-education.pdf).