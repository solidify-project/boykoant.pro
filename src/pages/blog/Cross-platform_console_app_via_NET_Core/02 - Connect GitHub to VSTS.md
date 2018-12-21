url:                blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS.html  
template:           blog-post.hjs

title:              Boyko Ant's Blog - Connect GitHub to VSTS

---

Hello everyone!

This article is the first in series of creating a cross-platform console app using .NET Core. To see the full list of articles available in current series, navigate [here](/blog/Cross-platform_console_app_via_NET_Core/Intro.html).

This article describes how to connect your GitHub account to VSTS and make your source code from GitHub available for builds and tests automation by VSTS.

Because we are talking about open source project there are no better place to host it than GitHub. And it's not because GitHub is free for open source projects and provides you with git source control, there are dozens of similar platforms that comply with those requirements. The biggest benefit for me is that it never was so easy to show your code to other people and invite them to collaborate. Also it helps with transparency - everyone can file an issue / enhancement and help authors to improve their project.

I also know that there are dozens of CI tools that also provide you with free pricing tier for open source projects and has first class integration with GitHub. But I decided to move forward with VSTS (aka Visual Studio Team Services) as a CI tool because of the following reasons:

- VSTS is free for team size up to 5 peoples. If you have MSDN subscription, you can access VSTS for free.

- VSTS comes with self hosted (aka cloud hosted) build agents with 240 build minutes per month for free.

- You can use build agents based on Linux, Windows and MacOS. It means that if you need to run some platform-dependent task you just need to choose the appropriate build agent for that.

So I decided to use GitHub to share my code and VSTS to automate builds and test runs. Potentially I can provide access to VSTS for very active contributors, but let's postpone this for now.

In the end my workflow with codebase will look like this:

- My master branch at GitHub is protected against direct commits. To contribute you need to create a pull request.

- Each pull request is recognized by VSTS and required test runs are started automatically.

- For now there are no integration from VSTS back to GitHub, so I need to go to VSTS to check the results of test runs for corresponding pull request. Then I need to go back to GitHub and either accept or reject pull request. It may not be the experience you expect, but let's consider this as a necessary evil for now.

- As soon as I have something new in my master branch, VSTS will recognize it and will start a build definition responsible for building a new application version.

- As soon as I've built the new version of my app it will be recognized by my release pipeline and release of the new version will be started.

So, back to the topic. 
To connect your GitHub account to VSTS, follow those steps:

### Step 1
Navigate to VSTS account and open the exact project you want to connect with GitHub.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/00.png" />

### Step 2
Click on settings and chose 'Services'.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/01.png" />

### Step 3
Click on '+ New Service Endpoint' and chose 'GitHub'.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/02.png" />

### Step 4
There are 2 options for authorization. I recommend to use 'Personal access token', because it will give you access to all repositories that your GitHub user has access to. To obtain GitHub personal access token, procced to the next steps.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/03.png" />

### Step 5
To generate a new GitHub personal access token navigate to GitHub. Under your user icon click on 'Settings'.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/04.png" />

### Step 6
Navigate to 'Developer settings'.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/05.png" />

### Step 7
Switch to 'Personal access tokens' and click 'Generate new token'.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/06.png" />

### Step 8
Now you need to provide an understandable token name together with required permissions, which are everything under repo, admin:repo_hook and user. Click 'Generate token' to generate GitHub personal access token.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/07.png" />

### Step 9
Now you have GitHub personal security access token. Copy it and paste to VSTS window (step 4) because you will be unable to see this token again.  

<img class="img-responsive" src="/assets/blog/Cross-platform_console_app_via_NET_Core/Connect_GitHub_to_VSTS/08.png" />

<div class="alert alert-danger" >
	I revoked this security token the moment after I took this screenshot. You should never ever show this kind of data to anyone.
</div>

Now you are ready to procced with next article, which will be about automating your test runs with VSTS.