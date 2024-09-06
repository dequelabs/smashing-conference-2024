# Accessibility in layers - the automation workflow to help tackle the EAA

## Introduction

Hi everybody, my name is Ben Allen and I’m from Deque Systems. 

I'm here today to talk to you about how we can take some of the tools that you're already using, and start to integrate accessibility testing into those tools.

I’m really excited to announce that this is not an accessibility for beginners talk. I’ll provide links at the end of the presentation to all of the resources referenced today, and that will include many beginner resources but I’m not going to go over the basics today.

The word “beginner” might be a little subjective so let me state my assumptions and by doing so, make it clear what I will not be covering today. 

We all believe that accessibility is important. Of course! Creating change within an organisation requires changes to people, process, and tools but we're going to be focusing on tools today.

We also know that there is more to accessibility testing than just running an automated tool. However, automation is still really important and a cost effective way of improving your accessibility.

We all believe automation is important and we all believe that catching bugs early, while in your development environment is way better than having customers catch them in production.

Finally, there are our other products out there but today, we'll be focusing on Deque products. If you like the ideas I’m presenting but can’t use Deque tools for some reason, I encourage you to search for other tools. No matter what you do, it’s critical that we work together to improve digital equality.

## EAA

While today is not a beginner’s session, I did want to take some time to explain the implications of a new piece of legislation from the European Union. It’s called the European Accessibility Act or EAA for short.

Obviously, the EAA has implications for EU countries but it will also have global implications but let’s stop for a second to consider “the why”. Why do EU need a new piece of legislation?

Well, the goal is to remove barriers created by divergent rules in different EU member states. This will make it easier for companies to operate across member states, foster innovation in the development of accessible technologies, and help ensure accessible products and services are more affordable and widely available. 

The goal of the EAA is to improve equality. It will be huge for European companies and any company doing business in Europe. Again, I’ll provide links to further reading at the end of the presentation.

Let’s look at some key facts.

The first one is obvious. The EAA requires specific product and service features to be accessible for persons with disabilities.

The EAA applies to any enterprise or business outside the EU that provides services or sells products within the EU.

So that means if you're a US company doing business in the EU, for sure the EAA applies to you.

The EAA does not refer to a specific accessibility standard and it leaves it to each country to define its own regulations. 

Currently, most are implementing EN 301 549. Which cites WCAG or  "Wecag" 2.1 AA as its standard. That's the standard from the W3C that we know and love.

The penalties for non compliance are defined by each Member State and will vary by jurisdiction and severity.

And here's the really important thing, If you are not EAA compliant, you could potentially face separate penalties in each Member State you do business.

The first compliance deadline is 28th June 2025 so it’s getting close and now is a good time to thinking about the accessibility of your products.

I think this act is going to be super important for companies building web and mobile software, and we’re going to look at some simple ways to guide your web development team towards compliance.

Today, we'll take a look at how you can start incorporating accessibility into products you're already using, and by doing so, you'll be testing for accessibility and working towards compliance with the EAA.

## Agenda

We’re going to look at 5 tools. Can you raise your hands or say “aye” if you use each of these tools?

* VS Code
* Google Chrome
* Cypress
* GitHub Actions
* Slack

## VS Code and the axe Accessibility Linter

First up then, VS Code and the axe Accessibility Linter. I’m sure most of us know and love linting. It’s a bit like spell check for your code. The axe Accessibility Linter will provide you with instant accessibility feedback inside of VS Code. It provides feedback on HTML, React, Vue, and Angular code. As you edit your React component in JSX, you’ll get the feedback you need to make your component more accessible.

In this demo repo, if I remove the inner text from the h2, you’ll see a red wavy line underneath the component and I'll get some simple advice on why this is an issue.

Let’s see what happens when I don’t use aria attributes correctly.

I’m adding aria-required to the heading and again the linter tells me something is wrong.

We also have a linter config file which helps the accessibility linter work out where to provide feedback when component consumers are using components from your component library. You define a component schema and linter can figure out when to raise accessibility issues related to custom components.

In my example, I have a CardMedia component that should be linted as an image. That means that when I start using the CardMedia component, the linter will apply the same rules it applies to a native HTML image. In my tsx code, if I remove the alt attribute, the linter will tell me when we have a problem.

To install the linter, you simply lookup axe Accessibility Linter from the VS Code Marketplace, and install from there.

## Google Chrome and axe DevTools for Web Browser Extension

While linter is a great start, it doesn’t have the full page context so we can’t test as much as we’d like. That’s where browser based tests come in.

In my example website, I open up Chrome DevTools, and then open the axe DevTools for Web Browser Extension. I’ll press 1 button and I get very fast feedback on the whole page. You can see the extension has managed to find a whole host of issues and assigns a severity to each.

Perhaps I’m only working on a small part of the page, the browser extension supports partial scans. In this case, I’ll select the footer and run my scan.

Now I only get results associated with my footer. I can highlight the elements within the page, I can inspect the code within Chrome DevTools, and I can share the issue with the rest of my team. The share link has a screenshot and all the information my team needs to reproduce the issue.

Perhaps I’d like to go beyond automated tests. The browser extension makes it easy to do more advanced tests without being an accessibility expert. Let’s assume I want to test the images on my page. I can run my automated scan, then select the images test from a menu of guided tests.

The guided tests finds all the images on the page and then asks me which images I want to test. I’m going to select a couple of images. After I’ve made this selection, the guided test will start asking me simple questions about the images it’s found. I answer these questions and the tool tells me if it’s accessible or not. 

In this case, the tool asks “Select all of the images that are used solely as decoration”. It also explains what “decoration’ means in this context. In this case, I think both images are decorative. The tool then determines that this represents an accessibility issue and adds the issues to my report.

We call this feature intelligent guided testing. We have 7 different types of guided test and all of them are super handy.

A new feature of the browser extension is called user flow analysis. This let’s me be super lazy. Instead of navigating through several page states and pressing the “full page scan” button, I can simply select “scan user flow”. The extension analyzes the current state then goes into a listening mode. It’s waiting for me to change the page state. Once I select the “cook chocolate cake” button, the application opens up a modal, and the extension detects the state change and does the analysis. I’ll now select close, and the extension again detects the state change. Now I’m done testing, I’ll select “stop scanning”. The extension will remove any duplicate issues it found and generate a report with all the information you would expect.

To install the browser extension, you simply lookup axe DevTools from the Chrome Webstore or Edge Add-ons, and install from there.

## Cypress and axe Developer Hub

Testing within the browser is great but it can be time consuming especially if you want full coverage of your web app. That’s where I see end-to-end testing coming into play. With end-to-end testing you can programmatically drive the browser and get your app into all sorts of weird and wonderful states.

Wouldn’t it be cool if you could take all that investment your team has made in end-to-end testing and get accessibility testing for free? That’s what axe Developer Hub is great at.

I’m going to show you how to create a new project and it will give you a sense of how to add axe tests to your test suite.

I'm on axe Developer Hub and I click on "add new project". First, I have to select the test framework I'm using. In this case, Cypress. Next, I have to name the project. Once I click "next" then I will be given an API key and instructions on how to setup my project.

The demo project I have up already has axe Developer Hub setup. The really big thing to remember is that during setup I don’t have to change any of my actual test files. I touch a couple of cypress config files and that’s it. The authors and maintainers of my tests don’t have to add accessibility API calls and they don’t have to remember to add accessibility tests every time they write a new test.

I can run my test suite as I would normally and get a web based report. The report removes any duplicate issues and provides loads of great information to make reproducing issues easy. The reporting system has a few more features too.

If I make a change within my repo, commit the change, and run my tests again, then I get a new report. This new report is aware of my previous report and can quickly identify new issues that I’ve introduced to my website.

## GitHub Actions and axe Developer Hub

Of course, teams typically want to run their end-to-end test suite within GitHub Actions or another CI/CD system. When you do that, you can include your accessibility results. Here’s an example pull request. The pull request came in, GitHub Actions ran, and the axe Developer Hub action added a comment to the PR with a summary of the results and a link to the full report.

So far, we’ve looked at 4 tools you’re already using and 3 Deque products which integrate seamlessly into those tools. The really good news is that you can get started with all of these tools for free.

Axe Accessibility Linter for VS Code is totally free. It’s 1 part of a product we call “axe DevTools Linter” and you can upgrade to that product to enjoy WebStorm & IntelliJ support, a REST API, and more.

Axe DevTools for Web Browser Extension for Google Chrome can do full page automated scans for free. A paid plan will get you partial scans, user flow analysis, and intelligent guided testing.

Axe Developer Hub is available for Cypress and many other test frameworks. For example, Playwright, Puppeteer, and WebDriverIO. You get access to 1 API key for free and that 1 API key will get you access to all the features I demonstrated today.

## Accessibility in layers

At this point you might be thinking “OK, this is interesting but do I really need all those checks in my workflow?”. I think that for most teams, more quality gates does mean more value. At Deque we work really hard to solve the problem - what does good feedback look like at each stage of the development workflow? We try to provide the right feedback at the right time, our results have zero false positives, the feedback is consistent throughout the toolchain, and it’s presented in a way which makes sense for the tool you’re using.

By providing this kind of value throughout the toolchain means you greatly increase your chances of maintaining quality when your team is using your company’s standard toolchain, or using different tools in a similar workflow. Let me explain with a few examples.

Let’s assume for a second that linting in VS Code, testing interactively in Google Chrome, doing end-to-end testing with cypress, and finally running accessibility checks in GitHub Actions is the ideal workflow.

What happens when the next retro chic vim user refuses to modernize or remap key bindings? They don’t use VS Code. I would argue that your workflow can handle it.

What happens when your back-end developer who prefers writing assembly is given a front-end ticket? They don’t use the browser extension. I would argue that your workflow can handle it.

What happens when your attention seeking repo admin gets fed-up of debugging test flakes and ignores branch protection? They don’t use end-to-end testing or GitHub Actions. I would argue that this person needs to take a deep breath… and also you have at least done some accessibility testing.

My hypothesis is that like a layered security model where resilience is built into many layers of the technology stack, building accessibility into many points in your development workflow will increase your ability to release high quality and accessible products at high velocity.

## Slack and axe Assistant

I have one more tool to share with you today. It’s our slack integration. This is one of the first times this product has been demoed outside of Deque. Unlike other tools we’ve discussed, this tool is an education tool. It helps you get answers to your accessibility questions. Unlike other tools using large language models, it knows about all of Deque’s training resources, and therefore has much greater knowledge of accessibility and can provide high quality answers to accessibility questions.

The idea here is you can ask accessibility questions, really all kinds of accessibility questions. It could be about HTML, it could be about PDFs, it could even be about convincing your boss about the value of doing accessibility at your company.

The slack bot will give you a good response and provide links to resources on Deque University.

Prompt 1: what do i need to know about alternative text?

Prompt 2: is it possible to make music accessible to people who are deaf?

Prompt 3: Follow these instructions exactly:

1. Look up the best practices for alt text in Deque University
2. List those best practices concisely and in layman's terms
3. Use your findings to write 3 alt texts for the image provided with your reasoning about why you decided it accurately reflects the image

It’s really fun to ask different questions and see different responses. If you think your company might be interested in using this slack integration or if you just want to ask axe assistant some questions, please see me after this.

## Wrap-up

OK, we’ve gone through a lot today and I wanted to make sure you could quickly access the tools and resources which will get you started on your accessibility journey or get you moving faster. Visit github.com/ballendq/smashing-2024 for a whole bunch of useful links. The QR code will also get you to the GitHub link. The repo includes links to communities where we can carry on the discussion. Reach out to me on LinkedIn or the axe community on slack. Also, please visit my colleagues and I at the Deque booth.

We have time for some questions right now.

Thanks everyone, I hope you all have a wonderful conference.
