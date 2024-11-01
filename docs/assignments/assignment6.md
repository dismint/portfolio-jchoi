---
title: Assignment 6
layout: doc
---

# Assignment 6 - User Testing & Analysis

## Task List

The tasks flow from top to bottom in order in how the user should perform them. Often times, higher tasks will set up lower tasks' state as needed.

| Task Title | Instruction | Rationale |
| :- | :- | :- |
| Onboarding | Please create a new profile and head to your profile page. | This task is meant to test the user's ability to create a new profile easily with the given UI, and navigate to what they think the profile page is (clearly labeled). |
| Profile Editing | Add some Webapps that you commonly use in your daily life! Label them as you please. Continue until you see fit! | This test is meant to test both the mechanics of how the webiste works in discovering the interface in which buttons to click to get actions to happen, as well as whether what the user thinks about the website is in fact, how they end up using it. |
| Webapp Editing | Edit one of the Webapps that you just added - change any fields that you see necessary | This task is placed to ensure that the user is able to again use the UI in an easy way to find out which steps need to be taken to perform editing - a crucial part of the app. |
| Webapp Deletion | Delete one of the Webapps that you just added | This task is placed to ensure that the user is able to again use the UI in an easy way to find out which steps need to be taken to perform deletion - a crucial part of the app. |
| Insight Gaining | Please look at the graph on the profile page and tell me patterns you might see - especially those that perhaps showcase connections that you did not think about previously! | This task serves not as something to do mechanically, but to see if the user is able to understand the purpose of the graph and what it is trying to show, and whether it provides any real value to the user (the purpose of the application). |
| User Interaction | Please go to the homepage and tell me something that other users have been doing, and what you think about their activity. | This task is meant to test the social part of the application, whether the "social media" section of the application serves its purpose in connecting uesrs in a meaningful and easy to understand way.


## Study Reports 

### Subject 1

The subject is younger (in middle school) and has significant experience with interacting in applications on the internet. They are likely to be able to quickly and fluidly grasp common patterns they have seen in other applications.

Up to the point of getting to the profile, everything went extremely smoothly as I expected. There were comments made about the styling of the UI (ouch) but nothing else. However, once the profile section started with the editing and Webapp interactions, there were some problems that started to arise. Firstly, there seemed to be a weird race condition on one of the updates of the graph library I was using where it would occasionally require the page to be loaded. This only happened twice however, and I was unable to reproduce it locally on my own machine. Otherwise, a point of struggle that I saw the user go through was the length of time it took to do each action. I had tested the functionality of the application, but didn't take time to do things like test Fitz's law. As a result, especially when they were going from clicking on "Add Webapp" to filling the forms to submitting, there was often a long gap of silence where it appeared they were falling into the same monotonous routine. 

There is of course, some merit in this system - after all it is stable enough to the point where once your muscle memory actives, the subsequent uses are quite straightforward. 

There was also a comment on how exactly the graph was visualized. When I was creating the graph representation, I simply randomly distributed the Webapps in a circle radius, and then connected the points. At the time, I thought that trying to make a nice automatic layout for the nodes would be a project in itself. However, the subject informed me that it would have been helpful just to have the nodes with similar tags be next to each other, that way they didn't have to zoom in and out so much to see the things they wanted in a given cluster. Although not simple, it was definitely a more reasonable ask that perhaps I should have incorporated into the original design. The subject had a good time looking at the posts of the other users, being able to perfectly tell what was going on. However, they commented that they would have liked more colors and clear communication through design.

One last thing I noticed while observing the subject was the time it took them to adjust to new UI features. In particular, on the profile page, I saw them clicking around and experimenting to see what each thing really did - in particular how the graph changed in response to adding or removing a Webapp. It was interesting to think about whether I should have had a tutorial or a more detailed list of instructions. My application actually has an info box about the item you selected, which initially starts out as a FAQ and guide when nothing has been selected yet. I think the information I provided was perhaps too basic, and it was not enough to truly convey what the UI features did. In the first place, the fact that I had this crutch in my application speaks to the fact that it is perhaps not the most user friendly design, and that there should have been more natural cues done through the design of the app.

### Subject 2

The subject is older (in their 40s) and has heavy experience interacting with few applications (high frequency uses of a few applications). They are likely to be able to quickly and fluidly grasp common patterns they have seen in other applications as well, but may be sucked into common workflows that they have seen on their subset of applications since they may not have had the breadth of experience that the younger subject has.

The subject interestingly had a hard time distinguishing from the login and register fields. Not for a significant time, but long enough to make me realize that they look extremely similar. Most people assume that the login field is on top and the register is on the bottom, but making sure that this is also conveyed through design is something important that I forgot to do, not just here but elsewhere on the application.

Unlike the first subject, this subject had a much easier time after the onboarding process. They were able to quickly use the aforementioned tooltip that I had to start adding and editing the nodes. 

The subject spent quite a bit of time looking around the application graph window and playing around by dragging the nodes to more spread out locations. This once again made me think that there was a potential issue with the graph layout - perhaps there should have been more time spent on this as a core feature of the application.

There was also a small bug that was discovered where deleting an items did not reactively refresh the view as it should have. It appears this was an oversight in my A5.

The subject happened to visit the homepage with posts naturally before I asked them to, and commented on how the post descriptions has IDs in them - this was an error on my end so I instead asked them to proceed as if they had correct names in them. When asked, they said they went to the homepage because it was where the page landed them at the very beginning. I thought this was an interesting point and noted it down as the landing page was not something that I had thought about in the slightest.

Subject also commented on how it would have been better if the posts had visuals. I had thought about this, but decided against it because I wanted to keep the scope of A5 reasonable, but similar to above, it seems to be a pivotal missing point based on the disappointment on their faces.

This user profile was actually able to notice something quite interesting about their graph because of the way Webber visualizes the graph as edges being the links. They noticed that there were two big groups of items (YouTube, Facebook, Milemoa) and (Costco, Amazon, Google Maps) that were linked within each other very much. They said this made sense because they tended to use each of these three things together in a similar time - in other words, it was likely when visiting one of the websites, they would visit the others as well. Another interesting insight that came up was the fact that Amazon and Facebook had many links to each other. They were able to theorize that perhaps one often acted as a gateway for the other to their respective groups.


## Design Flaws / Opportunities 

- Upon listening to users, it was immediately clear that more focus should have gone into the graph. In particular, the layout of the graph was not necessarily appealing and intuitive to gaining insights. Subject 1 did not mention anything in specific that they were getting out of the graph, even if Subject 2 found some interesting insights about their daily usage. This was a moderate physical design flaw - because the layout was random, it did not **lead** users to observations, rather it became the tool for users to make observations themselves. I started wondering after the interviews were done whether subject 2 even really needed the application to make insights, or if they simply did it because I was forcing them to think about it. I think that a way to solve this design would be to make it so that, as the subject suggested, I group similar Webapps together in the visualization. Of course, this is its own challenge on what it means for two Webapps to be similar.
- The next takeaway was a severe linguistic flaw in the lack of clear communication throughout the application. I do think that there were several good points in how I constructed the UI. The buttons to edit, delete, and add a node were all right next to each other, which made it very easy for the user to find. However, Subject 1 pointed out some flaws in the layout, mainly that they stayed together so closely no matter what. They thought that it should be the case the delete button or add button (or both) are put elsewhere since they carry weight in the application when you press them. In fact, they actually accidentally deleted a Webapp before I even told them to because they clicked on the button. Whether this was out of bad design or a mechanical misinput I did not ask, but regardless, it seems like a linguistic design that I should have thought about more thoroughly. Grouping of buttons and ideas together is a powerful concept we discussed in class, and looking back I wish that I had thought about it more for the project.
- There was an interesting point that was brought up by Subject 2 which was the fact that the landing page was the homepage where they could see the posts, and as a result they became more curious about this page, and navigated to it organically without myself telling them to do so. This made me think about a potential moderate linguistic as well as conceptual design flaw in how the application was structured. I had thought about how to lay things out on a page and also how to organize things in the big scope like the menubar, but I did not focus on the natural pathway that users would follow. I assumed a new user would take the path of register -> login -> profile -> add some apps -> view their feed. Of course, in this application it does not particularly matter whether this order happens or some other order does, but it was still surprising for me. After thinking about my design, I realized that there was no meaningful distinction between, for example, the tabs on my navbar, even though I would want users to go to the profile page first. It reminded me of something people always say about video games, which is that there should be no excuse for developers to text dump, since they can simply teach you anything in the medium of the game rather than text. In a similar way here, there is no reason that I should not be able to nudge users into the workflow I want through subtle designs. For example, I could have shaded the profile button when you had just logged in, or added tooltips as many applications and games do when you use them for the first time.


## Links 

[Deployment](https://a5-chi.vercel.app/)

[GitHub Repository](https://github.com/dismint/a5)
