# Week 8. Host and publish your map online
This week we are going to talk about using Github and publish your webpage online. We have already created interactive choropleth map using localhost, but our webpage is not publicly accessible yet. After this week, we will be able to publish it through github and every other people can see your geoviz.

## Github and Git
GitHub is website that provides hosting for software development version control using Git. Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. GitHub is not only a code sharing and social networking site for developers. It is also a web hosting site.  Below I have outlined how to host spatial data and a web application from GitHub.  This workflow is perfect for small applications. 

## Github pages
For this exercise, we will use Github to create a simple webpage repository. In this repository, we have the HTML, CSS, and JS required for our webpage. A feature of Github is the ability to create a homepage using something called Github pages.

To use Github pages to host a static page, you have to name your repository very specifically.The following steps detail creating a repository and setting up the initial settings.

Working with Github is easy, there are two main ways you can work with Github, via command line, or with a desktop GUI. The instructions below will show you how to get started on the command line.

## 1. Sign up a Github account
Sign up for a Github account on the Github site in which you can host projects and maintain repositories. ([Link](https://github.com/join?source=header-home))

## 2. Create, join, or fork repositories in your Github account
Repositories are project locations in Github. A repository is the most basic element of GitHub. A repository contains all of the project files (including documentation), and stores each file's revision history. Repositories can have multiple collaborators and can be either public or private. You can create copies of repositories that other people have created by ‘forking’ it from their account to yours. Repositories can have parallel versions called branches. The main branch is called the ‘master’ branch. Branches are used when you want to make try changes, but don’t want to change or break a working existing version of the code.

On the Github site, let’s create a repository. Repositories can be used for many projects, allowing you to collaborate, share, and modify scripts, programs, and websites. Project repositories can be named just about anything, and you should pick something relevant to your project. For example, if you are creating a repository to host your web geoviz, name it something like "geoviz" and use it for your project code and files.

## 3. Login and create a repository
Click on the Repositories tab on your main profile page. On your Github profile page, click on the Repositories tab.

i. In the upper right corner, select ‘New’. Create a new repository.

ii. In the Create a new repository window, set up your repository.
Name the repository ‘username.github.io’, and replace username with your Github username. Give the repository a description, make it public, and initialize it with a README. Don’t worry about the license at this point.

iii. Click Create.
You now have an empty repository set up in which you can add files and set up a project.

Let’s get Git setup so we can interact with it via command line on our local machine to create, edit, and manage files.

## 4. Check if Git is installed on your Machine
Moving back to our local machine, we need to get git and Github setup so we can work with it.

**If you are using Mac**: Using Terminal, we are going to check for Git, and if it is not found, we will download and install necessary files.

**If you are using Windows**: Git does not work easily from the Windows command prompt. To easily use command line to interact with Github, you need to install Github for desktop where you can use Git Bash. This is a command line interface that allows you to run commands to create repositories, rectify file differences, and push commits.

[Download Github Desktop](https://desktop.github.com/)

Once downloaded, proceed below, but instead of using Terminal, you use Git Bash.

#### i. Open Terminal/Git Bash
#### ii. Check git installation by entering the following command
`git –-version`
if you have Git installed, you will see the version. If you get an error, or you don’t see the version, you need to install Git. Install Git from the downloads page on the main Git project homepage.

https://git-scm.com/

Download Git for your machine. A wizard will lead you through the installation. You can select the defaults for installation. You might need to restart your machine after installation to get it to take effect.


## 5. Link your local webpage dictory with your github repository
Initiate your git, by typing `git init`
type in `git remote add origin <your reposity name, such as https://github.com/boehnert/webpage.git>`. For example, I create a repository with name of `choroplethlead`, then I just need to type `git remote add origin https://github.com/xiaojianggis/choroplethlead.git`. This command will link your directory on your local machine with the GitHub repository.  You will see this command on GitHub under how to push an existing repository from the command line.

## 6. Create a branch for your repository
Branch is just like a virtual environment. We can create a seperate environment and do experiment inside it. Now you need to create a branch called `gh-pages` from GitHub and switch to this branch. Type in `git checkout -b gh-pages`. This command with switch to the gh-pages branch in the repository.

## 7. Commit everything in your folder to your repository
Now just commit everything in the folder to your repository by typing in `git add .`, then type in `git commit -m 'This is my initial commit'`

## 8. Push your project up to the branch on the Github repository
Push your project up to the branch gh-pages by typing in `git push origin gh-pages`

## 9. Open your webpage on Web browser
Now your project is up on GitHub. In a web browser log into your GitHub account and view the project in the gh-pages branch. You can also view the web site using your http://<GitHub handle>.github.io/repository name. My final website can be viewed at https://xiaojianggis.github.io/choroplethlead/


## Homework
1. Finish the tutorial and create a interactive and dynamic geoviz. 
2. Using a the field of "num_bll_5p", different color scheme, and different scale of legend
3. Upload your `.html` file to the Canvas. 

**Reference**: 
https://gis.ucar.edu/github-web-hosting
