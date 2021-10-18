## Lab 8. Host and publish your map online

This week we are going to talk about using Github and publish your webpage online. We have already created interactive choropleth map using localhost, but our webpage is not publicly accessible yet. After this week, we will be able to publish it through github and every other people can see your geoviz.


## A little big more about Leaflet and web-mapping
### Add layer group on your map
In previous lab we added marker, lines, polygons, and geojson to the map. You may try to change the order of different layers. Here we can use the `leaflet` layer group to better manage the visibility of different layers. 

Step 1. Let first add two basemap layers based on Mapbox

Add the following script right behild your `L.map('map',..` statement in your previous lab.


```html
        L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', { attribution: '© OpenStreetMap' }).addTo(map);
        
        var mbAttr = 'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, ' +
                'Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            mbUrl = 'https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoibWFwYm94IiwiYSI6ImNpejY4NXVycTA2emYycXBndHRqcmZ3N3gifQ.rJcFIG214AriISLbB6B5aw';
            
        var grayscale   = L.tileLayer(mbUrl, {id: 'mapbox/light-v9', tileSize: 512, zoomOffset: -1, attribution: mbAttr}),
            streets  = L.tileLayer(mbUrl, {id: 'mapbox/streets-v11', tileSize: 512, zoomOffset: -1, attribution: mbAttr});
```
These statement just define two basemap layers, which we are going to add to our map.

Step 2: Add layer group for your markers

Let say you have defined several markers, 

```html
var temple = L.marker([39.981192, -75.155399]);
var drexel = L.marker([39.957352834066796, -75.18939693143933]);
var penn = L.marker([39.95285548473699, -75.19309508637147]);
```
Then you can group those markers into one layerGroup, 
```html
var universities = L.layerGroup([temple, drexel, penn]);
var universityLayer = {
    "Phily University": universities
};
```

Step 3: We can get started to add the layers to our map

In your geojson reading statement, after `L.geoJson...`
Add the following statement
```html
var overlayLayer = {
    "blood_lead_level": neighborhoodsLayer,
    "Phily University": universities
};

L.control.layers(baseMaps, overlayLayer).addTo(map);
```

You can now refresh your web page and check your map. 

### How to use the Lealet documentation
The leaflet has a very detailed documentation. While working on using leaflet to create web-based geovisualization, you should check the leaflet docmentation all the time. ([link] (https://leafletjs.com/reference-1.7.1.html)). You can find how to use different functions in leaflet functions; find different parameters and options. 

### What next for web mapping
Geojson is a good data format for your to save your spatial dataset. However, the Geojson is only suitable for small datasets and small number of features. Let assume you have tens of thousand or even more points to show on the web page. Using the `geojson` would make your system very very slow! In this case, using the database syste would make your system much more efficient. You can use the Postgres/PostGIS to manage all your datasets and then Leaflet can communicate with the database and show the features based on your requests. 



## Github and Git
GitHub is website that provides hosting for software development version control using Git. Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency. GitHub is not only a code sharing and social networking site for developers. It is also a web hosting site.  Below I have outlined how to host spatial data and a web application from GitHub.  This workflow is perfect for small applications. 

### Github pages
For this exercise, we will use Github to create a simple webpage repository. In this repository, we have the HTML, CSS, and JS required for our webpage. A feature of Github is the ability to create a homepage using something called Github pages.

To use Github pages to host a static page, you have to name your repository very specifically.The following steps detail creating a repository and setting up the initial settings.

Working with Github is easy, there are two main ways you can work with Github, via command line, or with a desktop GUI. The instructions below will show you how to get started on the command line.

### 1. Sign up a Github account
Sign up for a Github account on the Github site in which you can host projects and maintain repositories. ([Link](https://github.com/join?source=header-home))


### 2. Install Git and check if Git is installed on your Machine
Moving back to our local machine, we need to get git and Github setup so we can work with it.

**If you are using Mac**: Using Terminal, we are going to check for Git, and if it is not found, we will download and install necessary files.

**If you are using Windows**: Git does not work easily from the Windows command prompt. To easily use command line to interact with Github, you need to install Git bash for desktop where you can use Git Bash. This is a command line interface that allows you to run commands to create repositories, rectify file differences, and push commits.

[Download Github Bash](https://gitforwindows.org/)

Once downloaded, proceed below, but instead of using Terminal, you use Git Bash.

#### i. Open Terminal/Git Bash
#### ii. Check git installation by entering the following command
`git –-version`
if you have Git installed, you will see the version. If you get an error, or you don’t see the version, you need to install Git. Install Git from the downloads page on the main Git project homepage.

https://git-scm.com/

Download Git for your machine. A wizard will lead you through the installation. You can select the defaults for installation. You might need to restart your machine after installation to get it to take effect.


**For Mac**, type in `git --version` in your terminal and see if your get the git installed
**For Windows**, open your `Git` bash, and type in `git --version`. 

If we have the github account registered and `git` bash configured successfully, let get started and publish our geoviz online. 

**All the folowing commands will be run in Git Bash, NOT Anaconda**


### 3. Create a repository
i. Click on the Repositories tab on your main profile page.
On your Github profile page, click on the Repositories tab.

ii. In the upper right corner, select ‘New’.
Create a new repository, let's say you repo is call `bloodlead`. You can use other names as you like.

iii. In the Create a new repository window, set up your repository.
You name your repository as "geoviz" or other names you like. Give the repository a description, make it public. **Don't initialize it with a README.**

iv. Click Create.
You now have an empty repository set up in which you can add files and set up a project.

i. Click on the Repositories tab on your main profile page.
On your Github profile page, click on the Repositories tab.



### 4. Synchronize with your github repository
In you terminal, navigate to the directory that is storing your javascript files by using the `cd` command, my folder is called `geoviz`, you need to to use your folder name.
```
cd geoviz
```
Then initiate your folder as a github repository, 
```
git init
```
**MAKE SURE** your html file is named as `index.html`, or you will not be able to see your webpage.


Alright, let start to Synchronize our local folder with Github repository, 
```
git remote add origin https://github.com/xiaojianggis/bloodlead.git
```
You need to replace the last paramter by the link of your repository name. You can find these when your first created the github repository. This command will link your directory on your local machine with the GitHub repository.  You will see this command on GitHub under how to push an existing repository from the command line.

**Note**: if you get error of "fatal: remote origin already exists." Type the following statement to solve it,
```
git remote -v
git remote rm origin
git remote add origin https://github.com/xiaojianggis/bloodlead.git

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
In a web browser log into your GitHub account and view the project in the gh-pages branch.  You can also view the web site using your http://<GitHub handle>.github.io/repository name.  My final website can be viewed at https://xiaojianggis.github.io/bloodlead/

Make sure you replace the `xiaojianggis` by your own user name, and `bloodlead` by your own repository name. 



## Reference:
MIT DUSP Geoviz, https://github.com/civic-data-design-lab/16_11.S947/blob/master/week1/Part1_IntroGitAndGithub.ipynb
Web hosting on Github, https://gis.ucar.edu/github-web-hosting


