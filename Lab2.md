
# Lab 2 - laaS/PaaS architecture 
# Application Architecture 
Based on the scenario explained in lab instruction, the application architecture consisting of a web server written in Flask, a UI front end written in React, and a database layer consisting of Postgres is represented in diagram below:
As shown in architecture below, the Flask Web Server connects users with the database. All of the user requests are fetched and saved to the Postgres Database, and React UI is updated to show or change information based on what users do.
```mermaid
graph TD
    User -->|HTTP Requests| WebServer[Flask Web Server]
    WebServer -->|Database Queries| Database[Postgres Database]
    WebServer -->|API Calls| Frontend[React UI]
    
    subgraph Application Architecture
        WebServer
        Database
        Frontend
    end

```
# IaaS Deployment Architecture

```mermaid
graph TD
    User -->|HTTP Requests| LoadBalancer[Load Balancer]
    LoadBalancer -->|Distributes Traffic| WebServer1[Flask Web Server 1]
    LoadBalancer -->|Distributes Traffic| WebServer2[Flask Web Server 2]
    WebServer1 -->|Database Queries| Database[Postgres Database]
    WebServer2 -->|Database Queries| Database[Postgres Database]
    WebServer1 -->|API Calls| Frontend[React UI]
    WebServer2 -->|API Calls| Frontend[React UI]
    subgraph IaaS Infrastructure
        LoadBalancer
        WebServer1
        WebServer2
        Database
    end
```
# Description:
1. Initially, **Users** send HTTP requests to the system.
2. The **Load Balancer** then receives these requests sent by users and distributes traffic across multiple web servers to make sure of balanced load and high availability.
3. The **web servers** (Flask Web Server 1 and Flask Web Server 2) both handle user requests, run the application, and fetch or update data in the Postgres Database. They also send and receive information to and from the React UI.
4. Both web servers use the **Postgres Database** to store and retrieve data.THis database is managed within the IaaS environment that requires manual setup, scaling, and maintenance.
5. The **React UI** presents the user interface and receives API calls from the web servers.
6. In **IaaS**, we will be responsible for managing and setting up the load balancer, web servers, and database which increases the complexity of handeling the configuration, maintenance, and scaling of these components on our own. This approach gives more control over the infrastructure.

# PaaS Deployment Architecture

## Diagram

```mermaid
graph TD
    User -->|HTTP Requests| LoadBalancer[Load Balancer]
    LoadBalancer -->|Distributes Traffic| AppService[Flask App Service]
    AppService -->|Database Queries| Database[Postgres Database]
    AppService -->|API Calls| Frontend[React UI]
    subgraph PaaS Infrastructure
        LoadBalancer
        AppService
        Database
    end
```
# Description:
1. **Users** are responsible for sending HTTP requests to the system.
2. The **Load Balancer** receives these requests and directs them to the **Flask App Service**.It distinguishes the architecture with Iaas since the web application is hosted as a service (AppService) rather than as individual web servers.
3. The **Flask App Service**, a PaaS-managed service, runs the Flask application. It handles HTTP requests, interacts with the **Postgres Database** for data operations, and serves API calls to the **React UI**.
4. The **Postgres Database** has the similar role like in Iaas and acts as the data storage solution, accessed by the app service.
5. The **React UI** interacts with the app service for API calls and presents the user interface.
6. In **PaaS**, the **load balancer** sends incoming requests to one app service (Flask App Service) instead of splitting them between several web servers like in **IaaS**.
7. In **PaaS**, the service takes care of the load balancer, app service, and database, that makes us easy to focus on building our application instead of managing all of required parts.
   



