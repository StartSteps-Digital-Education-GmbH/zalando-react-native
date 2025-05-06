React Native Learning program - pilot curriculum planning doc
Background [confidential]
Zalando has developed a working prototype that integrates React Native views into our native
application. We aim to enhance this implementation to minimize cognitive overhead and improve the developer experience for both native and web engineers, who currently face challenges working within the existing setup. We expect the impact will be different for engineers working with Web, Android, and iOS native technologies at Zalando.

We believe this technology creates new opportunities for delivering features for more than one platform, targeting more customers. We also expect engineers to enjoy the shortened time to market for new features and less frustration caused by the technical debt of today’s App codebase. This technology will enable engineers to stay on top of industry trends and will position them at the forefront of software development. Some of the biggest technology players use React Native for their applications, including Shopify, Walmart, Instagram and Pinterest. 

Currently we are in a project phase of iterative and selected migration and in case of successful outcomes, and the decision to move forward with this technology, we would have ~164 engineers involved who are currently in the client teams (web engineers, Android, iOS engineers).
Learning needs [confidential]:
App Engineers (pilot group of 15-20 iOS and Android engineers): 
Our app engineers primarily use Swift for iOS and Kotlin for Android. 
Learning needs: Android and iOS developers need to learn CSS, Javascript, TypeScript and React fundamentals, as these are essential before working with React Native and building renderers at Zalando. 
For internal upskilling: They will also need to understand the high-level architecture of the Rendering Engine (A Zalando-homegrown, frontend framework which uses the React library for UI rendering and adds various platform capabilities on top. It is the core of Zalando’s web platform today and allows Zalando developers to easily create CX features for the Fashion Store and SSO UI on the Web and mobile Web), along with React and React Native frameworks, as well as the development workflow for building web-based features and screens. 

Web engineers (not part of the pilot):
Our web engineers are already using the Rendering Engine in their daily work. As Rendering Engine is built on React technology, which is very similar to React Native (same core concepts, same programming language), we expect that Web client engineers already have the skills to work with React Native. They will still need to learn the specifics of mobile app development, the development environment, and day-to-day developer experience (debugging, testing, releasing), which will differ from what they are used to when building web features and screens using Rendering Engine. 

Notes: Zalando dosnt use Expo.

Curriculum Overview:


Week 1: Prerequisites – JavaScript, TypeScript & React Fundamentals
Day 1 – Monday (Theory): Essential JavaScript & TypeScript
Topics Covered:


Modern JavaScript refresher (ES6+ features: arrow functions, destructuring, modules, promises, async/await)


TypeScript basics: type annotations, interfaces, simple classes


The goal is to ensure that all engineers have the modern JavaScript/TypeScript skills needed to write and read React code.


Day 2 – Tuesday (Practice): JavaScript/TypeScript Exercises
Activities:


Coding challenges in JavaScript


Converting plain JavaScript snippets to TypeScript


Practice with asynchronous operations (promises, async/await)


Handling API requests in TypeScript


Day 3 – Wednesday (Theory): React Fundamentals
Topics Covered:


Introduction to React: JSX, functional components, props, and state


Basic React Hooks: useState and useEffect


Goal: Build a solid foundation in the component model and state management underpinning React Native development.


Day 4 – Thursday (Practice): Building React Components
Activities:


Create simple “Hello World” React components


Practice passing data through props and managing state


Build an advanced functional component using hooks


Day 5 – Friday (Theory): React Strict DOM & Component Composition
Topics Covered:


Introduction to React Strict DOM: Overview and how it influences styling in React components


Best practices in component composition and code organization


Handling events and conditional rendering


Goal: Prepare engineers for the mobile mindset by reinforcing how to build clean, reusable components using Zalando’s preferred styling approach and to understand the impact of React Strict DOM (used internally) on both web and React Native components.



Week 2: Introduction to React Native & Capstone Project Kickoff
Day 6 – Monday (Theory): React Native Fundamentals
Topics Covered:


Overview: What is React Native? Differences from the web React


Core components: View, Text, Image, ScrollView
React Strict DOM + React Native as an example here and to keep it as close as possible with the Zalando mobile stack
Basic styling with CSS, Flexbox, and StyleSheet


Goal: Transition the mindset from web to mobile and understand the building blocks of a React Native app.


Day 7 – Tuesday (Practice): Your First React Native App
Activities:


Set up the development environment React Native CLI


Build a simple “Hello World” mobile app


Experiment with basic styling and layout


Day 8 – Wednesday (Theory): Internal Frameworks & Capstone Project Overview
Topics Covered:


Guest Session: A Zalando engineer will present an in‑depth look at internal technologies, including:


The Rendering Engine and how React is extended at Zalando


Zalando’s internal navigation framework (instead of React Router)


The internal state management solution and stateless Zalando UI modules


How React Strict DOM influences component styling across platforms


Capstone Project: Overview of requirements, architecture, and expectations
Note: we can work on project requirements with the Zalando team before the program starts, so it connects better with the project the Engineers will work on later


Goal: Connect the external React Native fundamentals with Zalando’s internal systems and set the stage for a real‑world migration project.


Day 9 – Thursday (Practice): Multi-Screen App Development
Activities:


Build a simple multi‑screen mobile app (using the internal routing/navigation framework concepts)


Customize headers, tabs, and transitions according to Zalando’s UI standards


Begin sketching out the structure for the Capstone Project


Day 10 – Friday (Theory): Data Integration & Asynchronous Operations in Mobile
Topics Covered:


Fetching remote data using fetch/axios in a mobile context


Handling asynchronous data with useEffect and managing loading states


Discussion: How do these principles apply when integrating Zalando’s backend services


Goal: Equip engineers to integrate external data sources into their mobile apps and refine the architecture for the capstone project.

Week 3: Advanced React Native Topics & Capstone Development
Day 11 – Monday (Theory): Advanced UI in React Native & Turbo modules
Topics Covered:


Deep dive into Turbo modules


Best practices for performance: avoiding unnecessary re‑renders, memoization techniques


Goal: Enhance user experience with smooth, polished interactions and learn to optimize performance.


Day 12 – Tuesday (Practice): Implementing Turbo modules & Performance Optimizations
Activities:


Turbo modules


Profile app performance and apply optimizations


Capstone Project: Finalize the project structure and core architecture


Day 13 – Wednesday (Theory): Accessing Device Capabilities
Topics Covered:


Using built-in libraries to access device features (camera, geolocation, sensors)


Basics of linking native modules and bridging when necessary


Goal: Prepare developers to incorporate native device features into their apps.


Day 14 – Thursday (Practice): Building a Device Feature
Activities:


Build a mini‑feature (e.g., a geolocation app or simple camera preview)


Experiment with third‑party libraries wrapping native functionalities


Capstone Project: Begin developing core components, UI layout, and navigation flows for the Project


Day 15 – Friday (Theory): Testing, Debugging & Deployment Overview
Note: We can change the topics on this day if Zaolando doesn't want us to focus on testing 
Topics Covered:


Introduction to debugging tools (React Native Debugger, console logging)


Testing using Jest and React Native Testing Library


Overview of app build, bundling, and submission processes (including CI/CD basics)


Goal: Equip engineers with strategies to ensure quality and prepare for the eventual deployment of Project Hermes.



Week 4: Capstone Project Completion & Hands-on Work
Days 16–20: Capstone Project Development 
Focus: Hands‑on development and troubleshooting with no dedicated theory sessions


Activities:


Iterative development of a Zalando‑specific mobile app that incorporates internal libraries and meets real‑world requirements


Code reviews and implementation of feedback sessions


Refinement of app architecture, advanced UI/UX, and performance optimizations


Integration of external APIs and handling of real‑world data


Final testing, debugging, and preparation for a presentation/demo


How curriculum will be genrated:

- We will have Folders, subfolders and files based on each topic and thier subtopics for example Javascript and Typescript can be one folder.

- only create subfolders when there is more than 3 related files to same topic

-subfolders can have thier own subfolders if needed

- the subflders inside a folder should be named [number]-[topic] the 2 digit numbering will be used to order the subfolders inside a folder


-Each topic(theory) will have its own md file That will be named [number]-[topic].md the 2 digit numbering will be used to order topics inside each folder


-Each folders has one genral Readme.md file that will have all the information and explination about that spesific lesson and will have link to other related md files

- The practicle sessions will be organized in subfolders named (Practice session) inside thier related topic folder which will include md files for instractions and code examples

- There is a main README.md file in the root directory which will have link to all topics organized on weekly basis, this will be used as man navigation to other md files(dont divide the topics of each week to days as the teacher will handel that and student dosnt nessory needs to know it)

- While the genral organization of files and folders will be based on topics, you have to consider the weeks and the days of the week as well so the program will run in order

- Follow best practices of Folder and files organization, markdown and online course content 
