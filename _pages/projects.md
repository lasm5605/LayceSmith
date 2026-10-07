---
layout: page
title: projects
permalink: /projects/
description: Currently working on...
nav: true
nav_order: 3
display_categories: [work, fun]
horizontal: false
---
# Layce Smith
## CSPB 3112 - Project Web Page

### Week 1 - Project Proposal

My goal for this project is to build a task management dashboard in React.

### Week 2 - Setting up the Environment

To begin this project, I installed node.js on my computer, which allowed me to install the JavaScript libraries. I also stood up the basic file structure in VS code using a Vite template for React.

### Week 3 - Version Control & Basic UI Design

In order to use GitHub for version control, I had to connect my locally saved project folders to a GitHub repository where I can push new commits. This required me to install Git on my computer and then set up a remote connection with the bash shell. Then, in following my project timeline, I went ahead and drew a wireframe of the application interface that I want to create.  

<img width="949" height="713" alt="image" src="https://github.com/user-attachments/assets/35418a2a-5b4a-412b-8674-d06ad5436840" />

My next step will be to dig into the React docs to learn more about their UI components and how to get started building out a simple interface.

### Week 4 - Building the Interface

Learning more about the React Components last week helped me better understand why components are so useful for building a task-management dashboard. Building a task dashboard entirely in HTML would require a lot of repetition since many of the dashboard features are things that appear again and again in very similar containers (individual tasks, task status, groups of tasks in lists, etc.). Components are javascript functions that return html code. Because they are functions, they can be reused, and any changes made to the function applies across all uses, which removes the problem of making the same change across large blocks of HTML code. Further, "props" (or properties) are another React feature that pairs with components. Props allow for different values to be passed into different iterations of a component, which is what makes the components reusable. Moving forward this week, I will be working on setting up the various components that I will need for my dashboard.

Another task I had set for myself this week was to practice using HTML and CSS to build out a simple interface. In attempting to do so, however, I realized that the Vite template I already downloaded in React includes HTML and CSS files that generate a dashboard when run. Since I'm not looking to reinvent the wheel and a solid interface file already exists, I will instead focus on adjusting that file to reflect the general layout that I want for my dashboard rather than build a new one entirely from scratch. For now, I have decided to adjust my dashboard design so I can get to work on the components and not spend a lot of time figuring out how to to get my dashboard to look exactly how I was originally picturing. Below are the modifications I will make to the React/Vite template to get my interface in a usable state so that I can start working on the backend a bit. 

## How I plan to reconfigure the Vite/React Interface Template

<img width="928" height="593" alt="Interface Template Changes to be Made" src="https://github.com/user-attachments/assets/8630e034-a30e-4037-b8ba-2eb23572f95e" />

### Week 5 - Implementing a Task Component and Task Lists

For the task component, I started by writing a simple function that displayed an item and a checkbox. The function was contained its own file and was set as the export default, so I could easily call the function in another file later. Then I realized that I can use Material UI, which is an open-source React component library that implements Google's Material Design. Material UI already has a checkbox component, so I copied the code into my own taskitem.jsx file, set it as the export default, and successfully imported it into my app.jsx file. However, I then discovered that Material UI also has a List component with a checkbox as a secondary option, so I decided to use that instead since it killed two birds with one stone (building a list and the individual list items with corresponding checkboxes). Then, I also saw that Material UI offers a text field component that allows user input, so I called that within the List component. Finally, I saw that Material UI has a container component, so I set my task list inside a container and added a button at the top of the container. This got me closer to my original dashboard design. I was also able to play around with the CSS elements within the javascript files to match colors and adjust spacing, alignment, etc.

My next steps are as follows:
* implement add and remove tasks feature
* create a second container to hold completed tasks

I used MidJourney to generate a quick, simple logo for my dashboard and used that to replace the React/Vite logo in the app interface template that I am repurposing.

<img width="1914" height="958" alt="image" src="https://github.com/user-attachments/assets/952706c0-0ba1-4e5c-b471-30b3e0f69468" />

### Week 5 - Diving into State Management/Information Flow

Last week I focused on familiarizing myself with the Material UI React Component Library to get an idea of what the UI could look like. This week was all about understanding states and props and how information flows between the components. 

Here is what I learned:

In React, parent/child relationships define how components (javascript functions) are configured in a tree, and this configuration is critical to state management, as state is shared by moving it up to the nearest common parent. Information flows down from parent to child: the parent controls a child's props, which are the data and functions it hands down. The child can display that data and call those functions to request changes, but the state itself stays with the parent.

Here is a diagram I created in FigJam that shows how my components will interact with each other:

<img width="641" height="686" alt="State Management Diagram" src="https://github.com/user-attachments/assets/329f6f88-0119-4d9c-95b3-9457a3879412" />
 
The parent component of my React dashboard is App. It passes data and functions to its children as props, which can be any JavaScript value. App owns two pieces of shared state: the tasks array and the selected filter. From these it calculates visibleTasks, which it passes to TaskList. It passes filter and a setter function to FilterTabs, which only displays the "To Do" and "Ta Da" buttons and reports which one is clicked. App also holds the functions that add, edit, and delete tasks and passes them down, so children can request changes without owning the data. TaskForm receives only the add function and keeps its own title state for the text being typed, and each TaskItem keeps its own editing state. App is the nearest common parent of the components that share tasks and filter, which is why that state lives there. 
 
NOTE: Eventually, tasks will be saved to localStorage so they persist after a refresh. 

With all of this in mind, I have started to reconfigure my component files. Although it was nice to play around with the Material UI React Components last week, the way I configured the components in order to make that visual does not align with the state management plan above. I will go back and build out the functionality and then can focus on reimplementing the design once I know that the functions are communicating correctly. 


