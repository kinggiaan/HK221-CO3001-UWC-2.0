# HK221-CO3001-UWC-2.0
**Team name** QLDA\
**Task 1**  Requirement elicitation\
**Task 2**  System modelling\
**Task 3**  Architecture design\
**Task 4**  Implementation - Sprint 1\
**Date:** November 9<sup>th</sup>, 2022 (task 4)

## Members
- Lê Tuấn Hưng (2052508)
- Mai Hữu Nghĩa (2052612)
- Trần Trí Đạt (2052443)
- Đinh Xuân Phú (2052650)
- Dương Gia An (1952163)

## Task 1
### Task 1.1
#### Context of Project
Service provider Y has hired Organization X to create the UWC 2.0 information
management system in order to increase the effectiveness of rubbish collection. Task
Management will be a part of the solution.

#### Relevent Stakeholder
-  Back Office
- Collectors and janitors
- Organization X
- Service provider Y

#### Expected jobs
- Back officer
1. Have an overview of janitors and collectors, their work calendar
2. Have an overview of vehicles and their technical details (weight, capacity, fuel consumptions, etc)
3. Have an overview of all MCPs and information about their capacity. Information should be updated from MCPs every 15 minutes with the availability of at least 95% of their operating time.
4. Assign vehicles to janitors and collectors
5. Assign janitors and collectors to MCPs (task)
6. Create a route for each collector. Assigned route is optimized in term of fuel consumption and travel distance.\
7. Be able to send message to collectors and janitors

- Collectors and janitors:
1. Have an overview of their work calendar
2. Have a detail view of their task on a daily and weekly basic. All important information should  be displayed in one view (without scrolling down).
3. Be able to communicate with collectors, other janitors and back officers. The messages should be communicated in a real-time manner with delay less than 1 second.\
4. Check in / check out task every day
5. Be notified about the MCPs if they are fully loaded.


### Task 1.2
#### Functional Requirement
1. Back officers
- View calendar
- View detailed information and manage the vehicle
- Get information about the MCPs
- Assign vehicles to collectors and janitors
- Assign collectors and janitors to MCPs
- Create route for each collectors
- Communicate with collectors and janitors
2. Collector and Janitors
- Check in and check out
- View calendar
- View tasks (daily, weekly)
- Get information about the MCPs
- Communicate with other collectors, other janitors and back officers

#### Non-Functional Requirement
1. Usability requirement
- Janitors and collectors can easily use basic functions immediately
- The back officers can use after 15 minutes training.
- Interfaces in Vietnamese, with an opportunity to switch to English.
2. Performance requirement
- The system must respond in less than 30 seconds. After 30 seconds, the system will notify the user.
- Can handle real-time data.
- Allow at least 100 users access at the same time without crashing.
- The task’s status has to be updated in 5 seconds when the janitors or collectors update it.
- MCPs information must be updated every 15 minutes.
3. Space requirement
- The system can handle 500 concurrent visits without any effect on the system efficiency.
- The system should be able to handle data from at least 1000 MCPs at the
moment and 10.000 MCPs in five years.
4. Availability requirement
- Working time of the system all days of the week, from 4am to 12pm.
- The system should not be down more than 10 minutes continuously, maximum 30 minutes a day.
5. Environmental requirement
- The system runs on internet browsing.
6. Security requirement
- Password require when login
- Encryption ensure with MD5
- Ensure not leak user information
7. Operational requirements
- System data is backed up every month to prevent data loss

#### Use-case diagram for the whole system
![Use case diagram for WholeSysTem](/Picture/Task%201.2.png?raw=true)

| Use Name             | Use Case: Task Assignment     | 
| ---                  | ---                       |
| **Created By**       | QLDA Team                 |
| **Date Created**     | Sep 18, 2022              |
| **Primary Actor**    | Back Officer              |
| **Description**      | Assign task for janitors and collectors |
| **Trigger**          | Click the button “Assign Task”          |
| **Preconditions**    | PRE-1. System available <br> PRE-2. Device connects to the Internet|
| **Postconditions**   | POST-1. Successfully assigned the janitor or collectors. <br> POST-2. Notify the task to the worker <br> POST-3. Record the task to the database  |
| **Normal Flow**      |  1. Back officer chooses the assignee. <br> 2. The system checks the availability of the assignee.<br> 3. Back officer choose day of work. <br>4. The system displays the info of all vehicles. <br> 5. Back officer chooses the vehicle for the assignee. <br> 6. Back officer chooses the MCPs. <br> 7. Back officer determines routes for the assignee. <br> 8. The system checks the availability of the routes. <br> 9. Send the notification to the assigned worker.|
| **Alternative Flow** | Alternative flow 1: <br> At step 2: <br> 2.a. Back officers can view the calendar to check the availability of assignee. <br>  <br> Alternative flow 2: <br> At step 4: <br> 4.a Back officers view the information of the vehicle <br> 4.b Back officers choose the vehicle for the assignee. <br>  <br>  Alternative flow 3: <br> At step 5: <br> 6.a Back officers view the information of the MCPs <br> 6.b Back officers choose the MCPs for routing. <br>   <br> Alternative flow 4: <br> At step 4: <br> 8.a Back officers can view the map to check the availability of the route. |
| **Exceptions**       | Exception 1: <br> At step 1: <br> 2.a. Assignee is not available <br> Return to step 1 in Normal Flows        |

#### Use-case diagram for Task Assignment Module
![Use case diagram for Task Assignment](/Picture/Task%201.3.png?raw=true)

## Task 2
### Task 2.1
First, we need to determine the process steps in Task Assignment.
In task 1.3, we have drawn the Task Assignment Module by Use-case diagram.
Process steps:
Go to Task Assignment → Choose worker → Choose available day → Pick the vehicle → Choose vehicle → Choose MCP → Create route → Notify to worker.
The below activity diagram captures the business process between systems and the stakeholders in Task Assignment Module.

#### Acitivity diagram for Task Assignment Module
![Activity diagram for Task Assignment](/Picture/Task%202.1.png?raw=true)

#### Diagram description:
1. Back Officer begin Task Assignment.
2. Back Officer choose the Worker (janitor and … who available) in the Worker List
that shows off by System.
3. Back Officer pick an available day of the chosen worker from the calender show
off by System.
4. System show MCP Maps then Back Officer do 2 activities parallel that assign
MCP and Check Available Route for the Worker in the chosen day.
5. Back Officer action Done task. Then, System check all information assign/pick by
Officer. If assigned information are Incorrect in 1 field (worker, day, MCP, route),
System will require Back Officer do all activities again.
6. Otherwise, if all information are Correct, System will notify all Information in 1
notification to Back Officer and Assigned Worker. (They can watch this
notification on their devices.)
7. End

### Task 2.2
#### Conceptual solution for route planning task
Our conceptual solution will be illustrated as the following step:
1. The back officer request to the controller to create a new route
2. The controller connect to Google Map API
3. If the connection fails, it will reconnect. If the connection is successfully
connected, Google Map will request data back from the controller
4. The controller them request data from the database
5. The database responds back to the controller with the data of MCPs location and
the collector’s location.
6. Then the controller will response back to the Google Map with the data
7. The Google Map then response back to the controller with the suggested route
options
8. The controller will send the options to the back officers for them to choose
9. The back officers choose the route then the controller will respond with the chosen
route.
#### Sequence diagram for route planning task
![Sequence diagram for route planning](/Picture/Task%202.2.png?raw=true)

### Task 2.3
In the class diagram, our group decided that there are 2 interface classes in the
Task Assignment Module called AssignTask and AssigningView (InfoView interfaces are
not included in Task Assignment Module, we draw it to make the system more
comprehensive).
#### Class diagram for Task Assignment module
![Class diagram for Task Assignment module](/Picture/Task%202.3.png?raw=true)

Task Controller is the bridge between User and private elements in Task. When we create task, there are 4 elements requires: worker information, date of assignment, route information (get from Google API), vehicle information.

## Task 3
### Task 3.1 
####  Architectural approach: MVC combined with Client-Server
The architecture design that we decide to use is MVC (Model-View-Controller) pattern. 
The MVC model contains three essential components:
- Model: contains the data logic represented by database (User Database, Order Database), can be modified by the Controller.
- View: consist of the user interface where users can view data from the Model and interact with the system through Controller (end-users UI and admin UI).
- Controller: acts as the brain of the model, it processes input events (user interactions), select View to display and manipulate Model data if necessary.

#### Diagram for Architectural approach

![Diagram for architectural approach](/Picture/Task%203.1.png?raw=true)

We choose MVC model due to the following reasons:
- First, MVC models support rapid and parallel development - Our system is divided into three separate parts which can be implemented independently.
- Second, the MVC model provides multiple views - Our restaurant site must display various forms of information which can be represented by different views from the model.
- Third, the MVC model is convenient for maintenance and modification - Our system demands dynamic changes. For example, adjustments in View do not affect the Model and Controller module.
- Fourth, the MVC model supports TTD (test-driven development) – Our system contains multiple features and components. As MVC is defined and structured properly, it enhances the testability of the whole system.

#### Architectural description
Our application architecture is based on an MVC model inside a Client-Server model. 
First, on the Client-side, the users of the system such as collectors, janitors and back officers will use their phone, laptop or computer to connect to the system through the browser of their devices. Through the internet, the users will interact with the interface of the website and send their request to the server. The server side will respond to the request through a MVC architecture. Moreover, if the request needs any data, the server-side connects to the database through a database server to receive any data that the users request. On the Server-side, we use MVC design patterns to illustrate our architecture design. 
Our design will contain 3 components as below:

- Controller: manages user interaction and passes these interactions to the View and the Model. Therefore, in our application, its main functions are mapping user actions to model updates and selecting views for displaying. 
- Model: is the central component of the pattern that directly manages the data, logic and rules of the application. 
- View: defines and manages how the data is presented to the user. That is, in our application, used to display their daily tasks, vehicle information, etc.

### Task 3.2
#### Implementation diagram for Task Assignment module
The diagram contains 1 application (Client), 1 main components (Server) and 1 component for calling Google API:
- Client: contains the **Browser** which will receive the requests from **Server** or send requests to **Server**.
- Server: consists of models interacting with database, view and controller parts.
- Google API: to create routes from MCPs

![Implementation diagram for Task Assignment module](/Picture/Task%203.2.png?raw=true)

#### Diagram flow
When users assign new task. Browser requests the assign form from the Task controller. Task controller gathers info from the models and manages to make Task view display the form (and lists when requested). In the assigning process, Task view will update and display new data which are set and gotten by Task model. Finally, when MCPs are chosen, the controller will request routes from Google API for the user to pick. 

## Task 4
#### Picture for the interface

![Picture for the interface](/Picture/Task%204.3.png?raw=true)
