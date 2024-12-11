---
title: "Project 6: User Testing and Final Release"
layout: doc
---


# Project 6: User Testing and Final Release
## Code


[Link to github repo](https://github.com/dismint/outfinity)


## Deployed App


[Link to deployed site](https://outfinity-dismints-projects.vercel.app/)


## User Testing Reports
### User Test with Will
During my user test with Will, several challenges and insights emerged. He had trouble distinguishing between the main closet and sub-closets when prompted to "look at what clothes you own." Initially, he hesitated, moving his mouse around the page, and then clicked into "College Clothes," commenting, "There are no more buttons on the page." After further prompting, he realized the "Main Closet" section could be clicked, noting that it looked more like a page heading than a button. This suggests that the layout could be clarified to improve navigation. Will also didn’t immediately connect the "Challenges" section with creating outfits for others. When asked to create an outfit for someone else, he first navigated to the "Outfits" tab and asked, "Do I make an outfit for you with my clothes?" This indicates that using someone else’s closet to make outfits was unintuitive. Later, when entering a challenge, he identified the "Find Challenges" tab correctly but was confused when he selected a challenge that belonged to his own account, which made him unable to participate in the challenge. This suggests users’ own challenges should be excluded from the "Find Challenges" section. Lastly, Will struggled with selecting clothes to add to a closet, assuming the app would automatically select all items, which he could then unselect as needed. He remarked, "How do I know if it's selected? I'll assume it's greyed out when not selected," highlighting the need for more intuitive colors or more familiar design patterns.


Despite these challenges, Will found the app’s visuals and interactivity both intuitive and appealing. He appreciated the dynamic nature of buttons, noting that their color change on hover helped him eventually identify the "Main Closet" button as clickable. He also liked the clean and visually pleasing layout, commenting that the design was "very cute and fits the purpose of the app well." He also found the organization of tabs and sections logical and remarked that the simplicity of the interface was helpful for understandability. He noted, "there are never more than a few buttons on the screen at a time." This made it easier for him to focus on tasks without having to read through or try out many different buttons, further contributing to the app's flow and overall usability.


### User Test with Ella
Ella found that many small, helpful indicators that are generally present in other applications were missing in Outfinity. In general, most of the testing went extremely smoothly, and there was no trouble creating an account or logging in. However, she said on many occasions, there was a lack of clear visual indicators that made actions confusing. One such example was for the action of finding clothing. The intended method in our application is to go to the main closet where a list of all your clothes is. However, she was more inclined to click on the New Closet and New Clothes button as those were clearly “dug out” in the UI, while the Main Closet looked more like a title header than a button that could be clicked on. Once she hovered, it was straightforward, but there were many comments about similar, unintuitive actions.


Ella did comment that the overall UI was very clean, and visually lent itself to be quite clear in where to go and what to look at.


Another point that Ella had was the lack of information that is given as a new user to the website. I had initially provided a very basic description of what the application was for, and she was quite confused at a number of specifics. For example, determining what clothes were required in certain scenarios to make an outfit, or create a challenge, or understanding the purpose of a minicloset. Some discoverability features were also lacking such as a hover effect on clothing, meaning that it was hard for her to find the possibility of clicking on clothing or items to inspect the particular element.


Overall, there are several things that would could improve on our application:


Clear visual indicators of certain actions like clicking into a new page or making a new item
Having much more text on the homepage and menus to describe what the purpose of each page is, and how it fits into the deeper functioning of the application.
Specify clear requirements, like needing a onepiece + shoes or top + bottom + shoes for an outfit.


### User Test with Elijah
During user testing with Elijah, we found that a lot of the conceptual sticking points we had anticipated in our user testing plan were a lot more confusing than we had thought. For instance, the idea of what exactly a “Challenge” was was initially unclear. When asked to “create an outfit for someone else on Outfinity,” like Will, Elijah initially navigated to his Outfits tab under the assumption that the task was to create an outfit using his existing clothing. Maybe the phrasing of the task could have used some work here too; Elijah mentioned that “It’s not clear to me that a challenge implies creating an outfit.” This seems to indicate that there is room to provide more guidance to users as they enter the app as to what the main purpose and what exactly a challenge is.


Elijah also mentioned when creating an outfit that the stacking mechanic wasn’t intuitive; he said it would be nice to be able to see all of the stacked clothes at once when viewing the outfit. While outfit stacking was something we struggled to design an implementation of, this indicates that there is definitely still room for improvement for user clarity.


Other than the conceptual confusion, Elijah found the rest of the app, particularly the concept of miniclosets and the process of adding clothes, to be very easy and intuitive. He also appreciated the design and said that overall the app looked very clean, which made it easier to navigate.


## Design Opportunities
1. Main Closet
- Level: Physical
- Severity: Moderate
- Flaw/Opportunity: When interviewees were directed to find all their clothes, two of them didn't realize that "Main Closet" was a button. Both Will and Ella were confused about this, and Will even clicked into a minicloset to look for all of their clothes. Afterwards, they both eventually realized that "Main Closet" was a button and not a header, because there was an animation when hovering.
- Cause: This is probably because when the "Main Closet" button isn't being hovered over, it resembles a stereotyipcal header. It doesn't have a distinct outline and has the same color as the background.
- Ways to Fix:
  - Add an outline to Main Closet to make it resemble a button
  - Make the Main Closet button area to have a different color from the background
  - Add a description at the top of the page differentiating the main closet from the miniclosets
2. Challenging Concept
- Level: Conceptual
- Severity: Critical
- Flaw/Opportunity: Both Will and Elijah were confused about the challenging concept. They weren't able to connect the fact that the "challenges" in the app allow users to create outfits for other users. Instead, Will and Elijah went to the "Outfit" tab to create outfits for other people and were confused because they would be creating outfits for other users using their own clothes.
- Cause: The challenging concept is very basic and across different apps it mostly describes an objective that needs to be completed and a winner is selected. In our app, it expands this, so our challenege is the notion of creating outfits for other users. This can be confusing to users, because we don't explictly describe how our challenges work.
- Ways to Fix:
  - Add an explanation of challenges on the Challenges page
  - Add a tooltip to the challenging page that describes that it's for making outfits for other people
  - Add an explanation on the Outfit page that emphasizes that it's for making your own outfits
3. What Constitutes an Outfit
- Level: Linguistic
- Severity: Minor
- Flaw/Opportunity: Ella had a hard time finding which clothes were needed in order to be able to make an outfit. Our app only tells the user whether or not the clothes picked out currently for an outfit is a complete outfit or not. This may cause users to keep clicking random clothes they don't want in order to be able to click the button to actually create the outfit.
- Cause: Although people in general know what outfits are like, our app requires a specific combinations of clothes to constitute an outfit. This isn't communicated to the user. The only thing the user knows is whether the outfit they have selected is valid or not, which isn't very clear on what more is needed for the outfit to be valid.
- Ways to Fix:
  - Add a description to the page where users pick an outfit that tells the user which combinations of types of clothes are needed to have a complete outfit
  - Add a red color border around the types of clothes that need to be added in order to have a complete outfit
  - The button currently only says "Incomplete - add more clothes" until the user picks a complete outfit, so we can rename this to "add a top" or bottom or the type of clothes they need to have a complete outfit


## Design Revisions
- We abandoned labeling and achievementing because we wanted to spend more time making sure the core concepts of the app work correctly and well. It doesn’t affect our impact case that much, because achievementing was used to encourage users to use the app and labeling was an idea that came from the VSD analysis.
- We also decided to allow the user to both search and filter by type of clothing within a closet. In P3, we envisioned doing this separately to make it not too complicated, but it makes more intuitive sense to do both at the same time.
- We decided to only let people submit one outfit per challenge to make sure that people don’t spam submissions. This allows them to put more thought into the one outfit they create.
- We decided that when a user unsaves an outfit they made, it essentially deletes it for them. This is because we wanted to have the notion of either having an outfit saved or not saved, so this simplified the concept more.


