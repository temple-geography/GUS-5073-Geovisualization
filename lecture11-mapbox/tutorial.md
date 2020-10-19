## Lecture 10. Host and publish your map online (II)
In this tutorial, we are going to publish our developed geoviz on Github. In previous tutorial, I assume you all have installed the Github desktop and Git bash environment successfully on your computer. 
**For Mac**, type in `git --version` in your terminal and see if your get the git installed
**For Windows**, open your `Git` bash, and type in `git --version`. 

If we have the github account registered and `git` bash configured successfully, let get started and publish our geoviz online. 

**All the folowing commands will be run in Git Bash, NOT Anaconda**


### 1. Create a repository
i. Click on the Repositories tab on your main profile page.
On your Github profile page, click on the Repositories tab.

ii. In the upper right corner, select ‘New’.
Create a new repository.

iii. In the Create a new repository window, set up your repository.
You name your repository as "geoviz" or other names you like. Give the repository a description, make it public. **Don't initialize it with a README.**

iv. Click Create.
You now have an empty repository set up in which you can add files and set up a project.

i. Click on the Repositories tab on your main profile page.
On your Github profile page, click on the Repositories tab.

### 2. Create a Directory for Github Projects on your Local Machine
Next we want to setup a Github folder on your computer that can contain local copies of our Github project directories. The easiest way to edit and change code is to work on it on your own machine. You can then sync the repository folders with the Github servers so others can see and use your code modifications, and you can pull changes others have made.

First, create a github directory on your machine. We are going to set up a github folder within the Documents folder of our local profile (documents/github) using Terminal and some basic command line to complete the task.

##### i. Open Terminal, change your current location to your Documents directory.
Use cd to change directories on your machine to the location you want to store documents.
```
cd you_dicrectory
```
**Note**: You can use `pwd` to find out your present working directory

##### ii. Create a new directory called ‘geovisualization’
Make a new folder that will hold our github projects.
```
mkdir geovisualization
```
This creates an empty folder called `geovisualization` in your folder. We will use this for storing local copies of our github repositories and as working space when we edit and modify your code and documents.

##### iii. Change the working directory to your new `geovisualization` directory
```
cd geovisualization
```
The ‘geovisualization’ folder is now your working directory and commands we run will be happening in this directory. We will work locally on our Github repositories in this space.

### 3. Clone an existing repo to your local computer
I prepare a repository on my github account, you can first use my code for this tutorial, but in your homework, you need to use your developed code. 

```
git clone https://github.com/xiaojianggis/geoviz.git
```
Then you will have a folder of `geoviz` in your directory. We are going to upload it to github. 

-------------------------------------------
**In your homewok, you need to start from here, forget about git clone**

If you want to upload your own web page to Github, you don't need to git clone anything, just `cd` to your folder of the code. **MAKE SURE** your html file is named as `index.html`, or you will not see your webpage.


### 4. Synchronize with your github repository
change your directory to the new created folder of `geoviz`. **In your homework, you need to change your directory to your code of the website**
```
cd geoviz
```
Then initiate your folder, 
```
git init
```

Alright, let start to Synchronize our local folder with Github repository, 
```
git remote add origin https://github.com/xiaojianggis/geoviztest.git
```
You need to replace the last paramter by the link of your repository. 

**Note**: if you get error of "fatal: remote origin already exists." Type the following statement to solve it,
```
git remote -v
git remote rm origin
git remote add origin https://github.com/xiaojianggis/geoviztest.git

```


### 5. Check out with a branch
Now you need to create a branch called gh-pages from GitHub and switch to this branch. Type in,
```
git checkout -b gh-pages
```
This command with switch to the gh-pages branch in the repository.

### 6. Add and commit your files to your repository
Now just commit everything in the folder to your repository by typing in 
```
git add .
git commit -m 'my initial commit, just a memo'
```

### 7. Finally push your project up to the branch gh-pages by typing in  
```
git push origin gh-pages 
```

### 8. Now your project is up on GitHub.  
In a web browser log into your GitHub account and view the project in the gh-pages branch.  You can also view the web site using your http://<GitHub handle>.github.io/repository name.  My final website can be viewed at https://xiaojianggis.github.io/geoviz/

Make sure you replace the `xiaojianggis` by your own user name, and `geoviztest` by your own repository name. 




## Reference:
MIT DUSP Geoviz, https://github.com/civic-data-design-lab/16_11.S947/blob/master/week1/Part1_IntroGitAndGithub.ipynb
Web hosting on Github, https://gis.ucar.edu/github-web-hosting

