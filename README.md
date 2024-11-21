# Child-Labor-Rotating-Chores-Home-Assistant
https://buymeacoffee.com/amandaworkb

![Screenshot 2024-11-20 214836](https://github.com/user-attachments/assets/cea71574-16ce-493b-b143-f13376fcee65)

This uses instructions from https://www.facebook.com/JediAndi/ and https://community.home-assistant.io/t/created-a-chore-tracker-with-points-system-in-home-assistant/316175 modified for our family.

### My goals: 

 - I wanted the kids to check off their chores.
 - I wanted them to earn points for each chore.
 - I wanted to be able to reset the chores each night- basically removing their "checks" and restarting the next day.
 - I wanted to be able to remove points for various reasons (Being sassy.)
 - I wanted a set of daily chores, a set of daily tasks to earn their tablet and a set of weekly chores.
 - Laundry chores will rotate each day for a particular child. Mondays are for Karen, Tuesdays for Max, etc.
 
 When you're done with this tutorial you will have the following:

 - Multiple views for each child
 - Testing view
 - One set of daily chores for each child.
 - One set of tablet chores for each child.
 - One laundry day for each child.
 - Sets of weekly rotating chore categories for each child.
 - One billion input boolean (toggles) for each chore for each child
 - Entities for each day of the week
 - Three time triggered automations
 - Three scripts
 - A partridge in a pear tree

 * If you're new, like me, once this is done you'll better understand how all of this works- conditions, visibility, 
 * editing entities within the code editor.
 
 * My advice would be to follow these instructions as I've typed them and then change things after to suit your needs.

 ### Programs used:

 - Home Assistant OS
 - Canva.com (if using pictures for title cards)

 ### Integrations Used:

 - Workday: https://www.home-assistant.io/integrations/workday

 ### Cards Used:

 - Picture-card (or) https://www.home-assistant.io/dashboards/picture
 - Markdown Card https://www.home-assistant.io/dashboards/markdown
 - Custom:Expander-Card: https://github.com/MelleD/lovelace-expander-card
 - Conditional Card: https://www.home-assistant.io/dashboards/conditional
 
 * Before getting started, I created a HOME dashboard. Then within the dashboard I made a view for each child with the sections option 
 	and 3 columns. 
 * Also to make things easier, create a TEST dashboard and check the "subview" option before saving. This hides the 
 	dashboard unless you're actively editing.

 ## Step 1a: Create Helpers for each chore FOR EACH child.
![Screenshot 2024-11-20 215044](https://github.com/user-attachments/assets/603b6e39-1614-4c10-afa4-266f7a08250b)

 (If you don't make the chore per each child then when one completes them- it'll mark it off for everyone. (My kids figured this out real fast and it was back to the drawing board.)
 For example: I have four groups; Kitchen Chores, Dog Chores, Bathroom Chores, and Vacuum Chores. In addition, I have tablet tasks (tasks they need
 to complete to earn tablet time, and daily chores.)
 
 Click settings > devices and services > helpers > toggle. 
 
 (I created the following:  Dishes, Clear Table and Load Dishwasher as three input booleans. I have four kids- Karen, Kara, Henry and Max. 
 So I then created Clear_Table_Karen, Clear_Table_Kara, etc. I kept the names all very similar- it helps later.)
 
 ## Step 1b: Add 'labels'
 ![Screenshot 2024-11-20 215002](https://github.com/user-attachments/assets/b4c3b42b-5fea-4ab4-9158-3a60bfc23379)

 Click settings > devices and services > entities.
 Choose the chore and open it. 
 Click the gear near the top.
 Add your label.

 (I labled every chore as CHORE and then added labels for each child and labeled their chores. This will help with automations and scripts.)

 ## Step 2: Create the chore counter
 
 Click settings > devices and services > helpers > create helper > counter and create a chore counter for each child.
 
 (I set the min value at -100 and max at 100. I'm hopeful but also a realist... I take points for shenangians.)
 
 Go back in and choose the counter inside the entities option (settings > devices and services > entities)- label it as before in step 1b.
 
 ## Step 3: Scripts

 Now we make a script for the adding, removing, and resetting of points.
 ![Screenshot 2024-11-20 215124](https://github.com/user-attachments/assets/1f45e3b8-9a8a-4989-846f-2075844b5eb1)

 Click settings > Automations and Scenes > Scripts.
 Click add script.
 Create new script.
 Add action- choose helpers.
 Choose counter.
 Click reset. 
 Under targets click choose label and choose "chores". (Everything with the label chore will be included. See- told ya it would help.)
 Label it as Reset Chores.

 Repeat these steps 2x to create a script that will increase and another that decreases. Choose increase/decrease instead of reset. Name them.
 (Unlike each chore, no need to create one for each child.)

 ## Step 4: Automations

 ### Step 4a: Increase and Decrease points

 Now we take the scripts and make automations for resetting the booleans each night. We will create one for each child.
 
 Click settings > automations and scenes > automations> create automation > create new automation
 Click When > Entity > State
 Choose every chore this particular child has.
 Scroll down to "Then Do"
 Click Add Action >helpers > counter > increment
 Choose the green "choose entity" option.
 Choose the child's chore counter.
 Label for each child. IE- Add Point Kara.
 Repeat this for each child.
 
 ### Step 4b: Reset Nightly

 Click settings > automations and scenes > automations> create automation > create new automation
 Click When > Click Time and Location > Time.
 Radio button = Fixed Time.
 Change the time to which ever time you want these chores to reset back to being "undone". I choose 4am.

 (This has nothing to do with points! This is just resetting all the chores.)

 Click Then Do > Helpers > Input boolean > Turn off > Choose gray "choose label" and choose "chores".
![Screenshot 2024-11-20 215203](https://github.com/user-attachments/assets/769462f4-9887-4263-98a0-a827185774b6)

 ## Step 5: Workday Automation

 Settings > Devices and Services > Workday (integration)
 Configure: Add entry > Label it Monday.	
 In the first line- 'Workday' uncheck everything except Monday.
 Under excludes, add everything except Monday.
 Repeat process for every day.
![Screenshot 2024-11-20 215401](https://github.com/user-attachments/assets/ce3973d2-96c0-4659-b02a-d0a663dd5b2b)
![Screenshot 2024-11-20 215352](https://github.com/user-attachments/assets/ce0eba75-d2e5-40ca-b387-2fa92afe2a1d)

 ## Step 6: Weekly Rotation

 ### Step 6a: Chore Card Visible Boolean
 
 Go to settings > devices and services > create helper > toggle
 Label this "chore card visible". No need for one for each child and no need to label with the chore label.

 ### Step 6b: Create a dropdown helper for the chore categories.

 Go to settings > devices and services > create helper > dropdown
 We are going to make one for each child. For the first child, make each categories and label it as Chore Visibility Off Reset (Child's Name).
 You can add labels for each child after by going back to entities and choosing their label if desired just like we did with chores.
![Screenshot 2024-11-20 215510](https://github.com/user-attachments/assets/f8559e0a-e7dd-41e6-9ceb-a91b9b7f8f15)

 ### Step 6c: Create the time triggers
![Screenshot 2024-11-20 215546](https://github.com/user-attachments/assets/73c90531-4a7c-41bb-9e91-7067cf193f1d)

 Go to settings > devices and services > automations > create automation > create new automation
 Under when, choose add trigger. Choose entity and then choose state. Type Monday for your state. This should pull up your workday entities we created.
 Under that, type in 'On' in the "TO" line.
 Then go to "Then Do" and click "add action" > helper > input boolean > turn on and choose Chore Card Visible as your entity. Save and call this Chore Card On.

 Go back to settings > devices and services > automations > create automation > create new automation.
 Under when, choose  add trigger >time and location > time > 12:01 am.
 Go to "And If" > add condition > time and location > time and choose Sunday. Leave times alone.
 Then choose "Then Do" > add action> helper > input boolean > turn off and the entity is "Chore Card Visible".
 Add another action > helper > input select > next and choose each child's Chore Visibility Off Reset entity.

 ## Step 7: Create cards

 (To make this easy and not as repetitious, use the TEST view and create a template card that can be copied into each
 child's view individually. We are going to create each individual card for categories (daily, laundry, bathroom, etc) and then add
 to some vertical stacks and expander cards ... ooh- pretty.)
 
 ### 7a. To start, go to the test view and choose any column. Click to add a new card.

 (I included copies of my yaml to help but you must change these to the entities you created above.)
 
 Choose custom:expander card. Add the yaml for the file "Daily Chores yaml". Choose one of your kids for this test example and make sure each chore has their name.

 ### 7b. Create another custom:expander card for Tablet Chores, Laundry and any of the categories you'd like. Choose the same child for each category.
 
 You should now have a column full of cards for one particular child.

 (*** Again, I used picture cards for my titles. The pictures are available within the yaml online.)

 ## 8. Copy To Expander and Vertical Stack Cards

 * Now let's get these looking pretty inside vertical stacks and condition cards. The condition card will show only the chores assigned each week.
 (I find it easier to open a second web browser window- open the test view in this second window as well. You're going to be copying and pasting A LOT.)
 
 ### 8a. Daily and Tablet Chore Cards
 ![Screenshot 2024-11-20 215640](https://github.com/user-attachments/assets/3902d48a-0223-4c96-af8e-c4efa83a8458)

 Go to another column in your test view. Click to add a new card and choose vertical stack.
 In the other window- choose the daily chores card and copy the yaml. (Highlight and click CTRL+C.)
 Go to the first window- where you make that vertical stack- leave title blank. Choose manual card, erase what's in the window and paste. (CTRL+V.)
 Click show visual editor. Click the + button to add another card. Choose manual.
 Go back to the other window and this time, copy the yaml for tablet time chores.
 Click save. This will be the daily stack of cards that will be always visible every day without changing.
 
 ### 8b. Now let's make your conditional cards that change.
![Screenshot 2024-11-20 215703](https://github.com/user-attachments/assets/6fd7dc92-fd30-4822-87b4-7d579aacbee7)
 In the window with the new cards created, click underneath to start a new card. Choose conditional. Click the 'card' header. 
 Go back to the window you're copying from and choose one of the rotating chore categories (kitchen, etc). Copy the yaml.
 Go back to the other window, choose manual card, remove  what's typed there and paste.
 Click back to conditions > add condition > and > click "add condition" right under the new "and"  > choose entity state
 Choose "Chore card visible" as your entity with state equal to "ON"
 Choose add condition underneath the new entity entry > entity state > chore visibility off reset (whichever child you've been using).
 Choose state equal to whatever category you're doing (kitchen, bathroom, etc).

 You now have your first card that rotates.

 Repeat this process (8b) for THIS child's other categories, making sure that you choose the right chore visibility category for each.
 
 ### 8c. Laundry card
![Screenshot 2024-11-20 215832](https://github.com/user-attachments/assets/5ee73d31-3930-47a0-b5ce-881a12ca0c59)

 Lets do the laundry card. This card only shows up once per week.
 Go under the cards you've created and click to add another card. 
 Choose conditional card.
 Go back to your other window and copy the yaml for the laundry card and paste this in the card section of the conditional card.
 Under conditions, choose entity state and the entity will be whatever day you want that child to do laundry. Type ON for the state.

 You should now have a column of chore categories. You can now copy this cards and paste into this child's view.

 ## 9. Next Child
 ![Screenshot 2024-11-20 215924](https://github.com/user-attachments/assets/d6cdd04b-ea02-4e11-b45f-e2cb0a880873)

 Now, go back to your test view. You are going to go into each card, go into the code editor, and change the entities for every
 chore to the next child. You do this by simply deleting their name and by starting to type the next child's name, it should start to auto populate.
 Do this for every chore. Change the laundry date for this child. Copy the cards and place into the next child's view. 

 Repeat for every child.

 ## 10. Counter

 * See file for the png for this card
 In each child's view, add a new card and choose Picture Elements.
 Under Card Options, upload the picture total_points.png
 Under Elements, delete the entity provided.
 Add new entity > choose state label
 Add the entity for the child's chore counter.
 See the yaml file for styling options.
