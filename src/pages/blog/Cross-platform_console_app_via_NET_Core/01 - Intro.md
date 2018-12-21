url:                blog/Cross-platform_console_app_via_NET_Core/Intro.html  
template:           blog-post.hjs

title:              Boyko Ant's Blog - Cross-platform console app via .NET Core

---

Hi folks!

With this post I plan to start a series of "how to" articles dedicated to creating a cross-platform console app using .NET Core, automating test runs, automating releases and all other cool stuff that you may want to have for your app. Each "how to" article will describe one particular topic and will be as much detailed as it can be.

If you don't want more detail what my app is about, you can jump directly to "how to" article using the following links:

1. [Connect GitHub to VSTS (aka Visual Studio Team Services)]()
1. [VSTS - Automate test runs]()
1. [VSTS - Improving task groups to increase reusability]()
1. [VSTS - Automate builds]()
1. Even more to come later...


## The APP
In my scenario I don't want to create yet another "hello world" app, I want to deliver something more or less useful to community and myself.

I was very excited with static site generators when I met them first time several years ago. They seemed so simple and brilliant, they were focused on one single task and they did it very well. I was even more excited because I planned to do something more or less similar back in 2008 when I'd just graduated from university.

Unfortunately I'm still unable to find a static site generator that complies with all my requirements. Usually my requirements are:

- Ability to work on any platform. I want to use the same tool in the same way on MacOS, Linux and Windows.

- Easy to use. In case I want to collaborate with my friends who are non-technical, I don't want to force them to read manuals so they can learn how to install and how to work with this tool.

- Logic-less templates. I don't want to have "spaghetti-code" in any of my projects. Sorry, but when I checked calendar last time it wasn't 90s anymore.

- Clear separation between view model and data model. As an engineer I want to bring several of my favorite best practices to non-technical people. Having dedicated roles of designer and content manager will definitely bring a lot of benefits in long-term perspective.

To sum up - one evening I got some free time, so I decided to reinvent the wheel. My friend used to joke: "You can't claim the honorable title of software developer if you haven't tried to rewrite jQuery at least once". That's how I ended up with this articles and, hopefully, the most fascinating reinvented wheel of all times.

P.S. The app itself is open source under MIT license and you can find it on <a href="https://github.com/solidify-project/engine" target="_blank">GitHub</a>. You are more than welcome to contribute to it. If you want to contribute, but don't know how (maybe you are not even a developer), just drop me a message.