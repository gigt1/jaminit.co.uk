---
categories: [Websites]
tags: [Jenkins, Jekyll]
title: Using Jenkins to Automate Your Jekyll Site
---
I recently thought about installing Jenkins on my home server to mess around with it and see what all the fuss was about it. I recently installed and let me tell you why and how I use it.

# Why I use it
I need a way to quickly build my site without building it locally, copying the files, finding the right directory and uploading them. I setup Jenkins to automatically build my site (the same way I would do it) as soon as I push to my Github repo. Surprisingly, Jenkins has inbuilt plugins for this type of thing and it was incredibly easy to set it up.
# How to set it up
## Installing Jenkins
1) First you need to get a copy of Jenkins from their website over at [jenkins.io/download](https://www.jenkins.io/download/). They have packages for Debian and other platforms pre built which you can just grab from APT which is nice and easy to do. You can also use the Java package if you're operating system doesn't have a package. I actually didn't realise there was a package for Ubuntu so I just went with the Java file.  

2) Next you want to run the server, to do this with the java file you simply run:
```bash
java -jar jenkins.jar
```
this will depend on how you've installed jenkins however.  

3) When you run it for the first time you need to go to `http://your-server-ip:8080`, you will be asked for an admin password to start the setup, this can be found in the console window where you started Jenkins (refer to step 2).  

4) Once you've done that you will be taken through the installation steps, its pretty self explanatory as you go down. When it asks you what plugins you would like, I'd suggest going with the defaults to keep everything simple.  

Well done! You've successfully installed Jenkins, now to setup our first job. I'm going to be setting this up for a Jekyll site but its fairly easy to create jobs for other languages.  

## Setting Up the Job
1) Once you've installed Jenkins head over to the  'New Item' button on the main page of Jenkins, for this tutorial we are going to be using a 'Freestyle Project' so select that. Also give you're item a name.  

![](/images/Jenkins-Create-New-Item.PNG)  
Above: You should be greeted with this screen, just input a name and you're good to go!  

2) Next you'll be greeted with a lot of options, we are going to scroll down to 'Source code management', choose git and enter the URL of your repo. Click the add button next to credentials and input your username and password for Github. You can leave all the other settings default in this section.  

![](/images/source-code-management-jenkins.PNG)  
Above: Input the URL of your Github Repo in the Repository URL Box  

3) After that, scroll down to build triggers and select 'Github hook trigger for GITScm polling', this is basically a Github webhook which we will configure later.  

![](/images/build-triggers-jenkins.PNG)  
Above: Select the 'Github hook trigger for GITScm polling' option.  

4) Now for the main part, we need to add some build steps, scroll down to this section and an 'execute shell' step, for jekyll all you need is the following:
```bash
gem install bundler jekyll
bundle update
jekyll build
zip -r build _site
```
The last command simply zips up the finished build so we can use it later.  

![](/images/execute-shell-jenkins.PNG)
Above: Input the commands into the commands box.  

5) Finally, all we need to do is add a 'Post build action', we need to add the 'Archive Artifacts' action, all this will do it make the finished zip downloadable. Make sure you input the name of the zip, in our case it is `build.zip`  

![](/images/archive-build-zip-jenkins.PNG)  
Above: Simply put `build.zip` in the files to archive box.  

6) Well done! You've finished setting up the Job, click save and it will take you back to the job home page. If you'd like, you can test your job now by clicking the 'Build Now' option on the sidebar.  

![](/images/build-now-jenkins.PNG)  
Above: You can click the 'Build Now' option if you'd like to test it

## Adding the Github Webhook
1) Now we need to go to your Github Repo, simply go to it and go to settings.   

2) Now go to the Webhooks section and click 'Add Webhook', if needed enter your password and continue.  

![](/images/webhooks-sidebar-github.PNG)  
Above: Click the webhooks link on the sidebar

3) You'll need to enter a 'Payload URL' this is basically your Jekyll install location with '/github-webhook' appended. For example `https://jenkins.example.co.uk/github-webhook`.  

![](/images/webhook-github-repo.PNG)
Above: Configure your webhook as follows.  

4) Leave everything else default and click 'Add Webhook'.  

You've done it! You've got your Jenkins installation to automatically pull and build your Jekyll site. If you don't want to automatically deploy your site, stop here or otherwise continue.  

## Automatically Deploying (Optional)
For this to work you're going to need a webserver already setup and working, you also will need PHP and shell access to your server. You don't have to do it this way and there is probably much more efficient ways to do this.  

1) First of all we need to download the 'Notification plugin' for Jekyll this basically enables us to quickly poll our webserver when a build is complete. You can do with by going to 'Configure Jekyll' and then 'Plugin Manager'.  

2) Once you've added the plugin head back over to your job you created earlier and go back to the 'Configure menu', notice how we've got a new section called 'Job Notifications', leave everything with the defaults apart from the URL field, here enter your domain and the name of the PHP file that you want to use (we will create it next).  

![](/images/job-notifications-jenkins.PNG)  
Above: Input the URL of your website in the URL box  

3) Lets create a bash script on your webserver, this is basically going to download the zip file, unzip it and move it to your webroot. Create a bash file called `download.sh` and put the following in:
```bash
wget "https://jenkins-url/job/name_of_job/lastSuccessfulBuild/artifact/build.zip" -P /var/www/html/ # This downloads the the file to your webroot
unzip -o /var/www/html/build.zip -d "/var/www/html/" # Unzips the zip
mv /var/www/html/_site/* /var/www/html/ # Moves everything from the _site directory
cp /var/www/html/_site/.htaccess /var/www/html/ # Moves the .htaccess file as well
rm -r /var/www/html/_site/ # Removes the _site folder
```

4) Head over to your web server and create a new PHP file with the name you used in step 2, I'm going to use `get-files.php`. All we are going to do is link to a bash file to run. Input the following to your php file:
```php
<?php
$output = shell_exec("/path/to/script/download.sh");
?>
```

You've done! You've completely automated the build process of your Jekyll website, now whenever you push to your github your site will automatically update without you having to do anything!
