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

# Building a React Task Dashboard

## Week 1 - Project Proposal

### Vision Statement

My goal is to transition from UX Research into Data Analytics by developing the skills to build custom, interactive dashboards. While tools like Power BI and Tableau are valuable for internal reporting, learning React will allow me to create more flexible, fully customized applications. Since I am covering other analytics tools in a separate course this semester, this project will focus on building a dashboard from the ground up.

### Motivation

I am excited to take a product from initial design through functional implementation. My experience has focused on designing user interfaces and researching usability; this project will allow me to expand those skills by bringing a design to life through code. Completing a fully functional application will be both a valuable learning experience and a rewarding professional accomplishment.

### Risks and Mitigation

Key project risks include scope creep, data loss, complex state management, and software bugs. I plan to mitigate these risks by:

- **Managing scope:** Prioritizing essential features within the 10-week timeline and pursuing additional functionality only if time allows.

- **Preventing data loss:** Using the browser's localStorage API to preserve task data between sessions.

- **Simplifying state management:** Following React best practices by minimizing redundant state and deriving values from existing data when possible.

- **Reducing bugs:** Developing incrementally and testing frequently to identify and resolve issues early.

### Project Assessment and Timeline

The project will follow a 10-week development plan, with flexibility to adjust as needed.

**Week 1:** Set up the React project using Vite in VS Code.

**Week 2:** Create a GitHub repository, sketch the interface, and learn React components, props, and state.

**Week 3:** Build the interface with HTML and CSS; implement task creation and deletion.

**Week 4:** Add task editing and completion functionality.

**Week 5:** Implement task priorities and due dates.

**Week 6:** Use localStorage to persist task data between sessions.

**Week 7:** Add filtering and sorting for overdue, high-priority, and completed tasks.

**Week 8:** Build a dashboard displaying remaining, completed, and overdue tasks; refine the visual design.

**Week 9:** Test functionality, resolve bugs, improve usability, and consider an additional feature if time permits.

**Week 10:** Deploy the application, document the project in GitHub with a README and screenshots, and add it to my portfolio.

This timeline provides a structured path toward a functional, polished application while allowing for adjustments based on progress and emerging challenges.


## Week 2 - Setting up the Environment

I began my project by setting up node.js as my runtime environment. Then I installed the React javascript library for components, and I installed Vite to act as both the development server and eventual build tool. From there, I was able to download a React frontend template and bundle and serve the code through the Vite development server. Vite has proven to be a great choice because it shows live updates in the development environment, which has simplified the debugging process considerably.

## Week 3 - Version Control & Basic UI Design

In order to use GitHub for version control, I had to connect my locally saved project folders to a GitHub repository where I can push new commits. This required me to install Git on my computer and then set up a remote connection with the bash shell. Then, in following my project timeline, I went ahead and drew a wireframe of the application interface that I want to create.  

<img width="949" height="713" alt="image" src="https://github.com/user-attachments/assets/35418a2a-5b4a-412b-8674-d06ad5436840" />

My next step will be to dig into the React docs to learn more about their UI components and how to get started building out a simple interface.

## Week 4 - Building the Interface

Learning more about the React Components last week helped me better understand why components are so useful for building a task-management dashboard. Building a task dashboard entirely in HTML would require a lot of repetition since many of the dashboard features are things that appear again and again in very similar containers (individual tasks, task status, groups of tasks in lists, etc.). Components are javascript functions that return html code. Because they are functions, they can be reused, and any changes made to the function applies across all uses, which removes the problem of making the same change across large blocks of HTML code. Furthermore, "props" (or properties) are another React feature that pairs with components. Props allow for different values to be passed into different iterations of a component, which is what makes the components reusable. Moving forward this week, I will be working on setting up the various components that I will need for my dashboard.

## Week 5 - Implementing a Task Component and Task Lists

For the task component, I started by writing a simple function that displayed an item and a checkbox. The function was contained its own file and was set as the export default, so I could easily call the function in another file later. Then I realized that I can use Material UI, which is an open-source React component library that implements Google's Material Design. Material UI already has a checkbox component, so I copied the code into my own taskitem.jsx file, set it as the export default, and successfully imported it into my app.jsx file. However, I then discovered that Material UI also has a List component with a checkbox as a secondary option, so I decided to use that instead since it killed two birds with one stone (building a list and the individual list items with corresponding checkboxes). Then, I also saw that Material UI offers a text field component that allows user input, so I called that within the List component. Finally, I saw that Material UI has a container component, so I set my task list inside a container and added a button at the top of the container. This got me closer to my original dashboard design. I was also able to play around with the CSS elements within the javascript files to match colors and adjust spacing, alignment, etc.

My next steps are as follows:
* implement add and remove tasks feature
* create a second container to hold completed tasks

<img width="1914" height="958" alt="image" src="https://github.com/user-attachments/assets/952706c0-0ba1-4e5c-b471-30b3e0f69468" />

## Week 6 - Rethinking Data Management/Information Flow

Last week I focused on familiarizing myself with the Material UI React Component Library to get an idea of what the UI could look like. The problem with the component-only interface, however, was that data was being handled within the components themselves rather than in state. Therefore, any rerender would result in a total data reset. I realized that configuration wouldn’t work for this project since a task management dashboard (at least how I am envisioning it) needs to support dynamic data that doesn’t get lost when a user closes their browser.

Here is what I learned about state:

In React, parent/child relationships define how components (javascript functions) are configured in a tree, and this configuration is critical to state management, as state is shared by moving it up to the nearest common parent. Information flows down from parent to child: the parent controls a child's props, which are the data and functions it hands down. The child can display that data and call those functions to request changes, but the state itself stays with the parent.

Rather than fixate on an aesthetic interface design, as I had done before, I built out a functional interface design.

<img width="641" height="686" alt="State Management Diagram" src="https://github.com/user-attachments/assets/329f6f88-0119-4d9c-95b3-9457a3879412" />
 
The parent component of my React dashboard is App. It passes data and functions to its children as props, which can be any JavaScript value. App owns two pieces of shared state: the tasks array and the selected filter. From these it calculates visibleTasks, which it passes to TaskList. It passes filter and a setter function to FilterTabs, which only displays the "To Do" and "Ta Da" buttons and reports which one is clicked. App also holds the functions that add, edit, and delete tasks and passes them down, so children can request changes without owning the data. TaskForm receives only the add function and keeps its own title state for the text being typed, and each TaskItem keeps its own editing state. App is the nearest common parent of the components that share tasks and filter, which is why that state lives there. 
 
NOTE: Eventually, tasks will be saved to localStorage so they persist after a refresh. 

With all of this in mind, I have started to reconfigure my component files. Although it was nice to play around with the Material UI React Components last week, the way I configured the components in order to make that visual does not align with the state management plan above. I will go back and build out the functionality and then can focus on reimplementing the design once I know that the functions are communicating correctly. 

## Week 7 - Project Mid-Semester Report

The functional interface design I created last week has helped me build my app to handle data in state (using the useState hook) rather than just within the components. In doing so, my app now has the following functionalities: 

- Input task title and add to the list of “To Do” tasks
- Edit each “To Do” task and either save changes or exit out of editing mode
- Delete each “To Do” task
- Click the checkbox of each “To Do” task, which assigns it to the “Ta Da” filter view
- Toggle between “To Do” and “Ta Da” filter tab views

<img width="565" height="481" alt="image" src="https://github.com/user-attachments/assets/81c58d12-1ccb-46f6-80cf-264e39bcdc3c" />

**Note:** adding a new task on the “Ta Da” filtered view adds a new task to the “To Do” view.

The functions I have already implemented seem to render correctly at this point. However, all the data disappears when the page refreshes. Therefore, the next thing I need to learn about and implement is saving the data to localStorage. Based on what I’ve read so far, there is a way to create custom hooks in React, and that seems to be the best way to save to localStorage, so I will begin researching and coding that functionality next. Once I have that key part of the project finished, then I plan to go back and work on adding a task priority feature and a task completion timestamp feature before making the UI look a little more polished. As of now, I feel a little ahead of schedule and am hoping to have time to come up with one bonus feature to add. Overall, I am feeling really good about what I’ve got so far.






