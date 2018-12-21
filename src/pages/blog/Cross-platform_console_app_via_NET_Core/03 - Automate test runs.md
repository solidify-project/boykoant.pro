url:                blog/Cross-platform_console_app_via_NET_Core/Automate_test_runs.html  
template:           blog-post.hjs

title:              Boyko Ant's Blog - Automate test runs

---

Hello everyone!

This article is the second in series of creating a cross-platform console app using .NET Core. To see the full list of articles available in current series, navigate [here](/blog/Cross-platform_console_app_via_NET_Core/Intro.html).

This article describes how to configure tests automation using VSTS for cross-platform console app created with .NET Core. The big detail here is not just to run those tests, but run them for each platform (Linux, Windows, MacOS) using different build agents.

You may wonder - why do I need to run my tests three times? Isn't .NET Core cross-platform and should behave the same way on each and every platform? Maybe it will be cheaper and faster to run those tests only once?  

The answer to those questions is yes and no. Yes, .NET Core is cross-platform and it works the same way everywhere, but it doesn't mean that it's also applicable to your code. One of the most obvious examples is using (or rather not using) Environment.NewLine to put a line break in text data. Also there are some differences in symbols that are allowed in your paths, I believe you get the idea. That is why it's better to test your app on each and every platform you plan to distribute it on.

Nowadays VSTS comes with self-hosted build agents based on Linux, Windows and MacOS (for now Linux and MacOS agents are in preview, but you can already start playing with them). So now you can easily configure 3 different build definitions and run all those tests the way you wanted. But, as a drawback, you will lose consistency and tractability. It will be better to have all your test runs inside one build definition, so you will have a single build (and tests) result (succeeded or failed) and have a way to easily trace everything back to the source code.

Let's start with configuring a simple single build definition for our automated tests.

	1. Create a new build definition from empty template. To do that navigate to your VSTS account and open one of your projects. Using menu on top go to 'Build and Release' area, inside go to 'Builds' area. Click '+ New' button to create a new build definition.
	



	2. Chose 'Empty process' template. I want to start with empty process on purpose, just to describe in more detail what needs to be done to make everything up and running.
	



	3. On 'Process' level we need to choose the name for our build definition and agent queue. For now they are not important to us, you can provide any values here.
	
	
	4. On 'Get sources' level I want to grab my sources from GitHub. In current example I will take them from repo called 'engine', which is within organization called 'solidify-project'.
	



	5. Now let's add those build steps using '+' button on a phase level:
		a. .NET Core Tool Installer
		b. .NET Core
		



	6. For '.NET Core Tool Installer' task I chose to install tool version 2.0.0
	



	7. For '.NET Core' task I firstly switch version of task definition to '2.* (preview)'. Then I switch command for 'test'. Then provided 'Path to project(s)' where my tests are located. Finally I double-checked that 'Publish test results' option is enabled.
	



	8. Now I can click on 'Save & queue' to save my changes and queue my first build. It can take some time for build to finish, so it's a perfect time to make yourself a fresh cup of coffee.
	



	9. Build is finished and everything seems to work perfectly. As you can see there are 35 tests and all of them are green, which is always a good sign.
	



At this point we already have a working build definition and it's about time to turn on a new feature (which is in preview for now). The name of the feature is 'Building with multiple queues'. When you turn it on it allows you to run one build configuration using several different agent queues, just exact what we needed to run our tests on 3 different platforms.

To enable a preview feature you need to follow those steps:

	1. Click on your profile icon and chose 'Preview features'.
	



	2. Switch scope from current user to account and turn on 'Building with multiple queues'. It may trigger page reload, but it's ok.
	



Now it's about time to adjust our build definition and use new feature we just enabled. In addition to that I also want to introduce a concept of task groups in VSTS. The idea behind task groups is simple - if you need to repeat the same steps a few times, you can put them in a group. It dramatically simplifies maintenance of repeatable tasks.

	1. Click on 'Edit build definition' button to jump back to build definition editor.
	



	2. Select 2 tasks that we already have in build definition and right-click on them. In menu that appeared click on '+ Create task group'.
	



	3. Provide a reasonable name for your task group, for example 'Build, test and publish results'. Also chose an appropriate group, for example 'Test'. After you will hit 'Create' button, a new task will appear under the name provided in selected category for all build and release definitions.



Now we need to add 2 more agents to our build definition and ask them to execute the same task group that we created a moment ago.

	1. Click on 'meatballs' icon on project level and then click on 'Add agent phase'. Repeat it twice, so you will have 3 agent phases in total.
	



	2. For each agent phase (including the first one) change the name of the phase (to, for example, 'Test (Linux)') and change agent queue in a way that for each phase you will have a new queue on top of a new platform. Another important thing to do - switch 'Run this phase' condition to 'Even if previous phase failed'. In that way you will always run all 3 phases, and if at least one test during phase 1 will fail it will not stop tests from phase 2 and 3 to run.
	



	3. Now you need to add a task group created during previous steps to 2 remaining agent phases. As I promised, you can find it under the name provided in previously selected tasks category.
	



	4. The final step will be to save build definition and queue it again. After a while you will see the results.
	



As you can see there were 35 tests and they ran 3 times. From 105 tests only 1 failed and it was on Linux platform. Despite the fact that our test failed on Linux, it doesn't prevent other tests run on other platforms. 
At the end of the day, my code doesn't seem to behave the same way on all platforms, even though .NET Core is cross-platform. But, lucky me, now I know where I have a potential bug and can investigate it.
