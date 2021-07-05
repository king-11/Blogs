## My Journey: Getting Selected in Google Summer of Code

# What is GSoC?

>Google Summer of Code is a global program focused on bringing more student developers into open source software development. Students work with an open-source organization on a 10-week programming project during their break from school. 

This post highlights **my journey** of getting selected into the program from the very beginning. I believe that there is no defined path for getting selected in such open-source fellowships. Everyone has a unique journey, and you can take a few things from other journeys to write yours :) because the essence of each one is similar.

![Let's get started](https://cdn.hashnode.com/res/hashnode/image/upload/v1625409867224/y_wlVPKZ2.gif)

Now that I have your attention, let's get started. I will talk about my journey in two parts: 
- the initial **Pre-GSoC** part will cover how I came about making my first contribution in Open Source and developed my skills
- the later part __GSoC InFocus__ focuses on GSoC specific things like selecting an organization, contributing, writing a proposal, etc.

# Pre-GSoC

This was a phase where I wasn't much worried about GSoC and focused on developing my skills, adding new tech stacks into my belt, developing more projects, and contributing to open source.

>This phase is crucial because your zeal and fire to contribute and make a mark in the open-source community starts to rage, and doing some fuels that fire further.

## How I came to know about GSoC?

The first time I heard about GSoC was in an event conducted by [Club of Programmers IITBHU](http://copsiitbhu.co.in/) where I was introduced to open-source programs like GSoC, Outreachy, etc. and people who were previously selected shared their experience with us. 

![conference](https://media.giphy.com/media/JUXtbHuixcZKeGJEro/giphy.gif)

I wasn't sure whether I would someday dwell into the realm of Open Source as, at that time, I was more focused on Competitive Programming like most of my peers. But things changed after the programming Camp in the Winter of 2019, where I started with Web Dev, and now I was sure I want to be amongst the group of people who clear GSoC.

Then came the GSoC'20. Many of my seniors who applied got selected, and I thought that a first-year student could never clear GSoC ( that perception changed this year :) ), so I focused on improving my skills in Web Development and didn't bother applying in 2020.

## Learning Phase

I was _burning the midnight oil_ to make web development my forte be it backend or frontend, vue or react, Django or NodeJS... I wanted to know it all as there existed so many fascinating things for me to learn.

![learning new things](https://media.giphy.com/media/3ohuAxV0DfcLTxVh6w/giphy.gif)

So here are some of the things I did to strengthen my skills in web development :

- I utilized [Frontend Masters](http://frontendmasters.com/) to cover most front-end things like frameworks and Design. Also took a git course by [@nnja](https://twitter.com/nnja)
- For Django, I started dwelling into the docs of [Django](https://docs.djangoproject.com/en/3.2/) and [DRF](https://www.django-rest-framework.org/) to learn more advanced features after completing basic stuff from [DjangoGirls](https://djangogirls.org/)
- Then, I did some projects using what I have learned to combine both backend and frontend. I did invest quite some time in them, and it was fun.
- Later on, when I came to know about things like NodeJS being faster and a more scalable DB such as MongoDB, I did a project using them in a [Hackathon](https://devfolio.co/submissions/peer-io-7356) with my friends [@Purushottam](https://github.com/m-e-l-u-h-a-n) and [@Madhava](https://github.com/dasari810), which we won too 🥳

>Apart from my own projects, I participated in projects of our Programming Club and also did an intern in a freelance project. These things prepared me to swiftly walk through a large codebase, collaborate on Github, use version control, apply my knowledge, etc.

## Open Source Hacktoberfest

>There couldn't be a better start for your open-source journey than [HacktoberFest](https://hacktoberfest.digitalocean.com/). It's an annual open-source event where project maintainers await your contributions, and they prepare their projects to accept new contributors.

Apart from contributing, you also get rewarded swags, tees, etc., by DigitalOcean and some of the projects. You can check out [hacktoberfestswaglist](https://hacktoberfestswaglist.com/) during hacktoberfest to know about projects offering additional swags.

I outlined my hacktoberfest with my friend [Kushal](https://github.com/K-Kumar-01) ahead of October. We decided to go good-first hunting, work on several issues and earn some swags. Who doesn't like swags, right? So I intended on completing the tasks to get those swags.

All of the projects were very welcoming. Even though I had **no idea** about the tech stack they were using, I contributed to them, but I focused on solving issues and asked many questions. 

![helping out](https://media.giphy.com/media/5wFjITVDtKD0wwJe7V/giphy.gif)

Some of my contributions which you can check out :
- [DX Heroes](https://github.com/DXHeroes/dx-scanner/issues?q=is%3Aclosed+author%3Aking-11)
- [Operation Code](https://github.com/OperationCode/resources_api/pulls?q=is%3Apr+author%3Aking-11+is%3Aclosed)
- [Datenanfragen](https://github.com/datenanfragen/website/issues?q=author%3Aking-11+is%3Aclosed)
- [Letra](https://github.com/jayehernandez/letra-extension/issues?q=author%3Aking-11+is%3Aclosed)

>By the end of October, I was familiar with contributing to open source projects, interacting with communities, finding issues, making PRs, and working my way around good first issues.

# GSoC InFocus

For most people, this phase is after and around December and January, where you start looking at organizations finding relevant and interesting projects to contribute to.

## Selecting Organizations

I started looking at GSoC archives in January and probably would have gone through the whole A-Z list about 10-20 times. Earlier, they didn't have filters for the tech stack, but they have it now, and it really helps to select the organization.

First, I jotted down the list of organizations I want to contribute to based primarily on my interest in their past and current projects and those that didn't require me to learn something completely new ( biggest mistake '-' ).

![filtered org list.jpg](https://cdn.hashnode.com/res/hashnode/image/upload/v1625384922319/dGkrSGMjD.jpeg)

One of the most useful tools I found when selecting my GSoC organization was developed by one of my seniors @[Nishant Mittal](@nishantwrp). With all the statistics at hand, I can filter out organizations.

%[https://www.gsocorganizations.dev/]

The list, as you can see, consisted of around 30-40 organizations. So I started filtering them out based on:
- Number of times org was selected for GSoC in past
- The tech stack they were working on should align with what I know, things like Javascript, Python, NodeJS, Rest APIs, etc.
- Number of students they select, which I filtered to be at least greater than or equal to 4.
- Amount of people already contributing to them because eventually only a few students will be selected for summer.
- Organizations using IRC as a means of communication were a *big NO!* for me.

In the end, I decided to go with [HTTP-APIs](https://github.com/HTTP-APIs). I started checking out their Contributing Guidelines, Resources to get started, and their repositories. I selected HTTP-APIs because REST APIs are my forte, and they were doing something pretty interesting.

I made a few contributions to their repos, upgraded their dependencies to support python v3.8 and updated Dockerfile. 

Still, a few things that took me away from them were that the mentors weren't that responsive, and even though I went through all of their resources, I couldn't find something significant to contribute.

So I drifted away from HTTP-APIs, but at the back of my mind, it was still that I have to make it work there somehow.

## Change of Plans

If you know me prior, you already know that I never went through with HTTP-APIs instead, it was [Chapel](https://chapel-lang.org/). Chapel is a programming language designed for productive parallel computing at scale.

The story behind the finding of Chapel is something that you don't hear often. I was in a meeting with my peers, and we started talking about things we are doing, and GSoC became a part of the discussion. 

My friend [@Jatin](https://codeforces.com/profile/rivalq) stated to me that, and I quote, "there is this language where you can run statements simultaneously using a `forall` loop". He seemed pretty interested, and so sparked the idea of taking a look at Chapel.

It was also at the same time, i.e. February, I was talking with one of my seniors [@Ashish](https://www.linkedin.com/in/ashishkr23438/), who previously got selected in GSoC under [OSGeo](https://github.com/pgRouting). My primary concern was that HTTP-APIs didn't work, and if I go in places related to Web Development there, the amount of already active students is way more than I wish to compete with.

![change of plans](https://media.giphy.com/media/9Dtye59YLYQpIwQWpv/giphy.gif)

So the plan I made after discussing with Ashish was to contribute to something, not JS, not Python, but things constituting C++, C, or some new language. And since Chapel caught my interest, I started there.

It is hard to find a project where you have experience with all the technical tools, so in hindsight, it’s okay for you to select an organization where you have only 40% of the tech stack down. You might even end up working with the part of the software that uses a language you have zero familiarity with, like me.

## Contributing to the project

The thing with all GSoC organizations is that they have excellent resources for you to get started with. This includes documentation, contributing guidelines, getting started with contributions, etc.

Just as HTTP-APIs, Chapel also had excellent resources for me to learn it, and I went straight for them started writing small scripts, learning the syntax incrementally.

The question you might have for me is why I decided to stick around with Chapel? The difference was chapel has so many issues *( over 2k )*, and these are the ones made by the core team itself. That made it pretty clear that I can contribute a lot and the team is highly active in developing the project.

I was observant even when reading the documentation and talked in the [gitter](https://gitter.im/chapel-lang/chapel) channel about how the documentation can be improved. I was also helping out by answering some of the questions in the channel.

![coding is fun](https://cdn.hashnode.com/res/hashnode/image/upload/v1625410769039/Am_Fu6jT4.gif)

Something that usually people forget about is interacting a being a part of the community. It's not just about coding your way around, and I made sure that I opened gitter every day to take a look at the ongoing discussion here as well as on Github Issues.

As chapel is a comparatively new language, I knew there could be scope for improvement on the implementation done in Modules. Also, at the time when I started contributing, I was pursuing courses on Algorithms and Operating System as part of my college curriculum.

So I went on to find the implementation of Quick Sort and Heap in the codebase, discussed few updates on them, and made a Pull Request.

After that, I started looking at existing issues, discussing how I should work them out, the idea of the core team about the issue, and eventually made the Pull Request for it to be reviewed.

The thing that kept me engaged in chapel was the quick response from mentors within a day or two. That made me feel that my contributions are very much appreciated.

## Writing Proposal

It is expected for a proposal to contain a detailed explanation of your implementation and timeline. What gives you an edge is your contributions to the project until then. This helps solidify the trust in your abilities to finish the project.

Even though I had drifted away from Web Dev, it all came back when projects that were announced by Chapel had a project on **Socket Library**. This was something that I was targeting since it was announced even before organizations were announced.

>Even though Chapel gave me a place to contribute to it was the project that kept me going because it's my niche and was something where I can apply all the knowledge I gathered over time.

I started working on my proposal after getting clarity on few things from my mentor on what were they expecting from the project. I also used to look out for questions that other people were asking related to my project.

![writing](https://media.giphy.com/media/XIqCQx02E1U9W/giphy.gif)

I got up to speed on working with sockets in `C`, went through the design of the socket library in `Python`, gathered more information about non-blocking sockets, and finally designed my proposal.

I made sure to add in code snippets and mock implementation of how the code will be implemented in `C` and `Chapel`. It is also a good idea to add in diagrams which I did, because images speak more than text.

My organization mentors seemed happy with the design because they didn't seem to have much issue with what I had shown them in the draft. 

But [@Shivansh](https://shivanshs9.me/), one of my seniors I requested to review my proposal, told me that it was less technical and needed more of it. This pushed me to improve my proposal further, add more details about the implementation, add in diagrams and code snippets.

You can find mine and several other accepted proposals in this repository. Courtesy of [Club of Programmers IIT BHU](http://copsiitbhu.co.in/)

%[https://github.com/COPS-IITBHU/GSoC-Accepted-Proposals]

## Post Proposal Submission

Going inactive after proposal submission shows that you aren't interested in the community, and you were doing it just for namesake.

I ensured that after proposal submission, I kept contributing and was active not that much but still had my presence in the channel. I wrote in my proposal that I would get all my pending PRs merged, and that's what I did.

Fast forward to 17th May, I was in a voice call when the result came out, and I literally shouted woohoo!

![gsoc result mail](https://cdn.hashnode.com/res/hashnode/image/upload/v1625417870501/Q4LP1LZBa.png)

# Final thoughts

GSoC is a non-competitive (after getting selected, of course 😏) program so try to cherish the community alongside it. Find your motivation; why do you even want to do it first, and the rest will follow.

GSoC is not an internship and should not be looked at as a way to earn money. It is definitely not something you should pursue half-heartedly or just for the sake of it, nor it would help you neither the community, and there can be better ways for you than open-source.

I am learning a lot from my mentors and fellow GSoC mentees. The community is something I will definitely enjoy and use my summer to learn from them and, as I say, make **Chapel go to Web**.

![that's all folks](https://cdn.hashnode.com/res/hashnode/image/upload/v1625418481704/4n4ZdmURx.gif)

Thanks for reading :) and please share your thoughts. I always like to meet more enthusiastic people, so do reach out to me on [Twitter](https://twitter.com/1108King) or [Linkedin](https://www.linkedin.com/in/lakshyasingh11/) to share your feedback or for any queries. I'd be more than happy to help and connect.

