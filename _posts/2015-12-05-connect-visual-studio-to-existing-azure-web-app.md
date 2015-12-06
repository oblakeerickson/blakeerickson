---
layout: post
title: Connect Visual Studio To Existing Azure Web App
summary: >
  The other day I spent way more time trying to figure out why I couldn't run
  Todo App locally than I really wanted to have. The main thing that was driving
  me nuts was that it worked fine the day before. The good news is that I figured
  out my issue which led me to write this post on how to enable SSL in ASP.NET Web
  API applications.  
tags: azure
---

When creating a new azure web application it is probably faster if you create your new web app from Visual Studio, but I like creating them from the azure portal since I'm usually in there already doing other management stuff. The problem is when I go back into Visual Studio to connect my new web app to azure it isn't quite clear the workflow to use to get your app deployed into azure.

## Step 1: Create a Web App Inside Azure

Sense we are already inside azure let's create a new web app:

1. Click on App Services in the left side bar
2. Click the Add button
3. Give the app a name
4. Click the Create button

![Azure create web app](https://blakeerickson.blob.core.windows.net/blog/00_azure_create_web_app.jpg "Azure create web app")

After you press the Create button Azure will provision your new web app. When it is done it will take you to the following screen where you can download the "Publish Settings" for your web app:

![Azure download publish settings](https://blakeerickson.blob.core.windows.net/blog/01_azure_get_publishing_profile.jpg "azure download publish settings")

## Step 2: Create a new Visual Studio Project

Now that we have our app created in Azure, let's create our app in Visual Studio.

Open up Visual Studio and select New Project:

![New Project](https://blakeerickson.blob.core.windows.net/blog/02_new_project.jpg "new project")

The "New Project" window should now be opened up.

1. On the right side un-check application insights (unless you want it). This part is actually kind of confusing because even though you can put in your azure credentials this section isn't for selecting your azure web app.
2. Give your project a name
3. Press OK

![Name Project](https://blakeerickson.blob.core.windows.net/blog/03_name_project.jpg "name project")

The "New ASP.NET Project - <project name>" window should now be opened up.

On this screen is where I was getting confused because we are going to be hosting our application in the cloud, but if you check that option, you have to create a new app instead of selecting from a dropdown of existing apps. For this reason we are going to leave this box unchecked and then press OK.

![Host in cloud](https://blakeerickson.blob.core.windows.net/blog/04_host_in_cloud.jpg "host in cloud")

Your project should now be creating:

![Creating project](https://blakeerickson.blob.core.windows.net/blog/05_creating_project.jpg "creating project")

Now open up Solution Explorer and right-click "Publish...":

![Publish](https://blakeerickson.blob.core.windows.net/blog/06_publish.jpg "Publish")

The "Publish Web" window should now be open. Press the "Import Button":

![Import](https://blakeerickson.blob.core.windows.net/blog/07_import.jpg "Import")

And browse for the publish settings file we downloaded earlier from our web app inside of azure:

![Browse](https://blakeerickson.blob.core.windows.net/blog/08_browse.jpg "Browse")

Once you have selected the file you can press OK:

![File Selected](https://blakeerickson.blob.core.windows.net/blog/09_file_selected.jpg "File Selected")

The "Publish Web" window should change to show the following screen with your app settings. Now press Publish:

![Publish](https://blakeerickson.blob.core.windows.net/blog/10_publish.jpg "Publish")

And now you are done. You have successfully created a web app inside of Azure Portal, downloaded the publish settings file, and connected it to a new Visual Studio project.
