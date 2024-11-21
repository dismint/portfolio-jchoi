---
title: P3 Convergent Design
layout: doc
---




# Project 3: Convergent Design




## Functional Design




Concepts that are in our app, but are not described in detail here because they're generic: Authing, Sessioning








::: tip CLOTHING
**Name:** Clothing[User]


**Purpose:** allow users to add items they own and keep track of metadata about each item.


**Operational Principle:** a user can upload a picture of an article of clothing they own such that this item will now be a part of their set of clothing, and will have type (hat, shirt, pants, etc.), name, and description specified by the user.


**State:**
```typescript
valid_types: set String
users: set User
clothes: users -> set Clothes
type: clothes -> one String
name: clothes -> one String
description: clothes -> one String
num_worn: clothes -> one Number
```
**Actions:**
```typescript
addClothing(t: String, n: String, d: String u: User, out c: Clothes)
    c not in u.clothes and t in valid_types
    u.clothes += c
    c.type = t
    c.name = n
    c.description = d


removeClothing(c: Clothes, u: User)
    c in u.clothes
    u.clothes += c
    c.type = None


search(searchType: String, searchUser: User, out clothes: set Clothes)
    searchType in valid_types
    returns clothes where c is in clothes if c.type is searchType for all c in searchUser.clothes


getType(c: Clothes)
    return c.type


wearClothes(c: Clothes)
    c.num_worn += 1
```
:::


::: tip OUTFITING
**Name:** Outfiting[Item, User]


**Purpose:** allows User u to group and refer back to a combination of Items which has certain restrictions on it.


**Operational Principle:** a user can group items together to create an Outfit, which must have one pair of shoes in addition to a top and bottom or one-piece. The user can then refer back to the Outfit item and retrieve all the Items in it.


**State:**
```typescript
users: set User
outfits: users -> set Outfit
contents: outfits -> set Item
name: outfits -> one String
description: outfits -> one String
```
**Actions:**
```typescript
addOutfit(items: set Item, u: User, n: String, d: String, out o: Outfit)
    u.outfits += o
    o.contents = items
    o.name = n
    o.description = d


removeOutfit(o: Outfit, u: User)
    o in u.outfits
    o.contents = None
    u.outfits -= o


addItemToOutfit(o: Outfit, i: Item, u: User)
    o in u.outfits
    o.contents += i


removeItemFromOutfit(o: Outfit, i: Item, u: User)
    o in u.outfits and i in o.contents
    o.contents -= i


getContents(o: Outfit, out contents: set Item)
    return o.contents


getAllOutfits(u: User, out outfits: set Outfit)
return u.outfits
```
:::


::: tip COLLECTIONING
**Name:** Collectioning[Item, User]


**Purpose:** a User can group Items into groups representing a set or subset of items they own.


**Operational Principle:** after a User creates a Collection, and before they delete it, the user can add items to the Collection such that when the user views the Collection, the item will be there.


**State:**
```typescript
users: set User
collections: users -> set Collection
contents: collections -> set Item
name: collections -> set String
```
**Actions:**
```typescript
createCollection(u: User, n: String, out c: Collection)
    u.collections += c
    c.name = n


deleteCollection(c: Collection, u: User)
    c in u.collections
    u.collections -= c
    c.contents = None
    c.name = None


addItem(c: Collection, i: Item, u: User)
    c in u.collections
    c.contents += i


removeItem(c: Collection, i: Item, u: User)
    c in u.collections and i in c.contents
    c.contents -= i


getContents(c: Collection)
    return c.contents


getByNameAndUser(n: string, u: User)
    return c in u.collections if c.name = n


getName(c: Collection)
   return c.name
```
:::








::: tip CHALLENGING
**Name:** Challenging[Collection, Item, Submission, User]


**Purpose:** allow a User to ask other users to submit Submissions based on a set of restrictions specified by the original user, and allows the original user to pick winning entry or entries.


**Operational Principle:** after a user creates a Challenge with restrictions given by a specified Collection and optional Item, it will be available for other users to see and submit Submissions to. Then, the original user
can select one or more winning entries after ending the Challenge.


**State:**
```typescript
users: set User
challenges: users -> set Challenge
restriction: challenges -> one Collection
must_include: challenges -> opt Item
entries: challenges -> set Submission
owner: entries -> one User
active: challenges -> one Bool
```
**Actions:**
```typescript
createChallenge(u: User, r: Collection, opt i: Item, out c: Challenge)
    u.challenges += c
    c.restriction = r
    if i: c.must_include = i
    c.active = true


endChallenge(c: Challenge, u: User)
    c in u.challenges, c.active = true
    c.active = false


selectWinners(c: Challenge, u: User, winners: set Submission, out winningUsers: set User)
    c in u.challenges, c.active = true
    winner in c.entries for winner in winners
    return winningUsers where u in winningUsers if entry.owner = u for entry in winners


enterChallenge(c: Challenge, u: User, entry: Submission)
    c in challenges, entry not in c.entries
    c.entries += entry
    entry.owner = u


getRestriction(c: Challenge)
    return c.restriction


getMustInclude(c: Challenge)
    return c.must_include else None
```
:::


::: tip LABELING
**Name:** Labeling[Item, Collection]


**Purpose:** provide information about an Item from a predetermined set of labels and filter items within a grouping of items.


**Operational Principle:** if a Label is added to an Item by a user and not removed, then filtering on the Label will display the Item and any other Items with that Label within a Collection. Available labels are predetermined.


**State:**
```typescript
valid_labels: set String
collection: set Collection
contents: collection -> set Item
labels: items -> set String
```
**Actions:**
```typescript
addLabel(i: Item, l: String, col: Collection)
    l in valid_labels and i in col.contents and l not in i.labels
    i.labels += l
   
removeLabel(i: Item, l: String, col: Collection)
    l in i.labels and i in col.contents
    i.labels -= l


filter(l: String, col: Collection)
    l in valid_labels
    returns items where i is in items if col.contents includes l for i in items
```
:::








::: tip ACHIEVEMENTING
**Name:** Achievementing[User]


**Purpose:** allow a User to be rewarded for good behavior and display these awards to other users.


**Operational Principle:** after a user behaves in a way that should be encouraged, they are given an achievement that reflects this behavior and is visible to other users.


**State:**
```typescript
all_achievements: set String
users: set User
user_achievements: users -> set String
```
**Actions:**
```typescript
system addAchievement(a: String, u: User)
    a in all_achievements and a not in u.user_achievements
    u.user_achievements += a


getAchievements(u: User)
    return u.user_achievements
```
:::




### Synchronizations
```typescript
app Outfinity
    include Authenticating
    include User from Authenticating
    include Sessioning[User]
    include Clothing[User]
    include Clothes from Clothing
    include Outfiting[Clothes, User]
    include Outfit from Outfiting
    include Collectioning[Clothes, User]
    include Collection from Collectioning
    include Challenging[Collection, Clothes, Outfit, User]
    include Challenge from Challenging
    include Labeling[Clothes]
    include Achievementing[User]


sync register(username, password: String, out user: User):
    User.register(username, password, user)
    Collectioning.createCollection(user, “main closet”)


sync login(username, password: String, out user: User, out s: Session):
    when User.authenticate(username, password, user)
    Sessioning.start(user, s)


sync logout(s: Session):
    Sessioning.end(s)


system sync authenticate(s: Session, u: User):
    Sessioning.getUser(s, u)


sync addClothes(tag: String, name: String, description: String, u: User, col: Collection)
    c = Clothing.addClothing(tag, name, description, user)
    Collectioning.addItem(col, c, u)
    main = getByNameAndUser(“main closet”, u)
    Collectioning.addItem(main, c, u)


sync removeClothes(c: Clothes, u: User, col: Collection)
    Clothing.removeClothing(c, u)
    Collectioning.removeItem(col, c, u)
    main = getByNameAndUser(“main closet”, u)
    Collectioning.removeItem(main, c, u)


sync searchClothes(type: String, u: User, out clothes: set Clothes)
    return Clothing.search(type, u)


sync addOutfit(items: set Item, u: User, n: String, d: String)
    validate that Clothing.getType(item) for all item in items creates a valid set of types
    Outfiting.addOutfit(items, u, n, d)


sync removeOutfit(o: Outfit, u: User)
    Outfiting.removeOutfit(o, u)


sync addItemToOutfit(o: Outfit, c: Clothing, u: User)
    Outfiting.addItemToOutfit(o, c, u)


sync removeItemFromOutfit(o: Outfit, c: Clothing, u: User)
    validate that Clothing.getType(i) for all i in Outfiting.getContents(o) remains a valid set
    of types after removing c
    Outfiting.removeItemFromOutfit(o, c, u)


sync wearOutfit(o: Outfit)
    contents = Outfiting.getContents(o)
    for item in contents Clothing.wearClothes(item)


sync createCollection(u: User, name: String)
    validate name != “main closet”
    Collectioning.createCollection(c, u, name)


sync deleteCollection(c: Collection, u: User, name: String)
    validate that Collectioning.getName(c) != “main closet”
    Collectioning.deleteCollection(c, u)


sync createChallenge(u: User, r: Collection, opt i: Item)
    Challenging.createChallenge(c, u, r, i)


sync endChallenge(c: Challenge, u: User, winners: set Outfit)
    Challenging.endChallenge(c, u)
    Challenging.selectWinners(c, u, winners)


sync enterChallenge(c: Challenge, u: User, entry: Outfit)
    restriction = Challenging.getRestriction(c)
    items = Outfiting.getContents(entry)
    validate that i is in Collectioning.getContents(restriction) for i in items
    if Challenging.getMustInclude(c) validate that Challenging.getMustInclude(c) in items
    Challenging.enterChallenge(c, u, entry)


sync label(i: Item, label: String, col: Collection)
    Labeling.addLabel(i, label, col)


sync removeLabel(i: Item, label: String, col: Collection)
    Labeling.removeLabel(i, label, col)


sync searchByLabel(label: String, col: Collection)
    Labeling.filter(label, col)


sync addAchievement(a: String, u: User)
    Achievementing.addAchievement(a, u)


sync getAchievements(u: User)
    Achievementing.getAchievements(u)
```


### Dependency Diagram
![Dependency Diagram](https://i.imgur.com/WfGgRLW.jpeg)


## Wireframes
[View wireframes here.](https://www.figma.com/design/gzyVfmdF3eoCU2VraTes75/Outfinity?node-id=0-1&m=dev&t=GCSYb4wwQstOdo2Z-1)
## Heuristic Evaluation
### Usability Criteria
**Discoverability:** The wireframe does a good job for discoverability in several places like uploading clothes, looking through your closets, etc. However, there’s a potential confusion when users click on a challenge from the home page. Instead of being taken to a detailed page about the challenge, they are directed straight to the submission page. While this flow is a great accelerator, making it easy for users to submit outfits, it may feel disorienting initially. One way to address this is by adding an intermediate page that provides more details about the challenge, including its description and a preview of the challenge author’s closet. Alternatively, the flow could be adjusted so that clicking on a challenge navigates users to a detailed challenge page, while retaining the accelerator by adding a “Submit Outfit” button directly on the home page challenge card. This way, users can both quickly participate and have access to more context if needed.


**Accessibility:** On the challenge submission page, our team prioritized making the clothing images as large as possible to accommodate users with motor disabilities. This design choice also helps all users by making it easier to see the details of each clothing item. However, this approach trades off with the absence of the challenge description on the submission page. Without this description, users may have a hard time referencing specific details while creating their outfit, forcing them to navigate back to the original challenge page and lose progress. To address this, we can add a dropdown button on the submission page to show the challenge description. This solution gives the flexibility of having the description and having the pictures of the images be as large as possible.


### Physical Heuristics
**Mapping:** The wireframe has good mapping in many areas, especially in the logical arrangement of clothing items. For example, the app tries to mirror how clothes are worn on a person, from top to bottom, as much as possible. However, this design isn’t fully used on the challenge submission page. When users are selecting items for their outfit, it could feel more intuitive if clothing options were visually arranged in the order they are worn—hats at the top, then tops, pants, and shoes. The hard part is that this arrangement could limit the number of options displayed for each clothing type, limiting creativity. Additionally, searching for a specific item might require more navigation. A potential solution is to have tabs for clothing types on the side of the submission page, arranged top-to-bottom to match the human body. This way, users can intuitively navigate options while maintaining access to a broad range of choices.


**Situational Context:** In the original wireframe, user profiles only displayed badges already earned. However, this didn’t provide enough situational context about overall progress or motivate users to achieve more. To improve, the team decided to include all possible badges on the profile page, with unearned badges grayed out. This gives users a clear sense of accomplishment and encourages them to collect more badges. The trade off is that showing all badges can make the interface visually cluttered and potentially overwhelming.
### Linguistic Level
**Information Scent:** Information scent is one area the wireframe could improve on. For instance, filtering options in the user’s closet could display the number of items available for each filter. If users are searching for tops, for example, the filter could show how many tops are in their closet. Similarly, when tagging outfits by occasion, users could see the number of outfits they’ve saved for each occasion. This extra information would help users get a better sense of their wardrobe and spot occasions where they’re short on outfit options. They could then create challenges based on this information to get new outfit ideas for those occasions.


**Consistency:** When considering how to display clothing items for selection, our team explored existing dress-up apps for inspiration. Many of these apps use a tab system where each tab displays clothing options for a specific category, like tops or bottoms. This familiar layout allows users to easily browse and select items. Adopting a similar tab-based format for our app would be consistent with existing patterns, making the experience more intuitive. It would also improve discoverability by aligning with users’ expectations based on other apps they may have used.


## Visual Design Study
![Color](https://i.imgur.com/FD4obsm.png)
![Typography](https://i.imgur.com/WOYLDqd.png)


## Project Plan
Concept Order:
1.  Authing, Session given to us
2. Clothing
3. Collectioning [Clothing, User]
4. Outfiting
5. Challenging
6. Labeling
7. Achievementing


| Concept         | Task                                          | Date          | Person        |
|-----------------|----------------------------------------------|---------------|---------------|
| Authing, Session| Import base code                             | 11/21 (Thurs) | Justin        |
| Clothing        | Implement concept class                     | 11/22 (Fri)   | Annie/Justin  |
| Clothing        | Implement related API calls                 | 11/25 (Mon)   | Annie/Justin  |
| Clothing        | Implement basic frontend                    | 11/27 (Wed)   | Annie         |
| Clothing        | Implement styling                           | 12/4 (Wed)    | Justin        |
| Collectioning      | Implement concept class                     | 11/22 (Fri)   | Tiana         |
| Collectioning      | Implement related API calls                 | 11/25 (Mon)   | Tiana         |
| Collectioning      | Implement basic frontend                    | 11/27 (Wed)   | Tiana/Jennifer         |
| Collectioning      | Implement styling                           | 12/4 (Wed)    | Justin        |
| Outfiting       | Implement concept class                     | 11/22 (Fri)   | Tiana         |
| Outfiting       | Implement related API calls                 | 11/25 (Mon)   | Tiana         |
| Outfiting       | Implement basic frontend                    | 11/27 (Wed)   | Tiana/Jennifer         |
| Outfiting       | Implement styling                           | 12/4 (Wed)    | Justin        |
| Challenging     | Implement concept class                     | 11/22 (Fri)   | Jennifer/Tiana      |
| Challenging     | Implement related API calls                 | 11/25 (Mon)   | Jennifer/Tiana      |
| Challenging     | Implement basic frontend                    | 11/27 (Wed)   | Jennifer      |
| Challenging     | Implement styling                           | 12/4 (Wed)    | Justin        |
| Labeling        | Implement concept class                     | 11/29 (Fri)   | Annie         |
| Labeling        | Implement related API calls                 | 12/2 (Mon)    | Annie         |
| Labeling        | Implement basic frontend                    | 12/4 (Wed)    | Annie         |
| Labeling        | Implement styling                           | 12/5 (Thurs)  | Annie         |
| Achievementing  | Implement concept class                     | 11/29 (Fri)   | Tiana         |
| Achievementing  | Implement related API calls                 | 12/2 (Mon)    | Tiana         |
| Achievementing  | Implement basic frontend                    | 12/4 (Wed)    | Jennifer      |
| Achievementing  | Implement styling                           | 12/5 (Thurs)  | Jennifer      |
| Overall         | Style navbar and home page                  | 12/4 (Wed)    | Justin        |
| Populate Data   | Add clothes to app to simulate multiple users’ closets, create simulated challenges | 12/5 (Thurs) | Everyone      |
| Task List       | Create task list for users to follow for user testing | 12/5 (Thurs) | Annie         |




We plan to not implement concepts that are not super necessary to our app if things are taking longer than expected. The first one we expect to drop is Achievementing. In the worst case, we can also not implement Labeling. Other functionality that isn’t super important is certain pages like a page for one clothing item and stats.


The other concepts we believe are integral to the app’s functions, particularly Challenging; if we foresee difficulties implementing this concept, we plan to have those of us who are working on non-essential concepts switch their focus to implementing Challenging well.




