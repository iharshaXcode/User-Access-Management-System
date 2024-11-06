# User Access Management System

This project is a web-based User Access Management System that enables an organization to manage user access to various software applications. It allows users to register, request access, and receive approvals from managers, with administrative functionalities for system and application management.

## Features

- **User Registration**: Allows new users to sign up and create an account.
- **User Authentication**: Registered users can log in based on their assigned roles.
- **Role-Based Access**:
  - **Employees** can request access to software applications.
  - **Managers** can approve or reject access requests.
  - **Admins** can create new software applications and manage system settings.
- **Access Request System**: Employees can submit access requests to software applications.
- **Approval System**: Managers have a portal to approve or reject access requests.

## Technologies Used

- **Backend**: Java Servlets, JSP
- **Database**: PostgreSQL
- **Server**: Apache Tomcat
- **Frontend**: HTML, CSS, JavaScript

## Project Structure

```plaintext
.
├── src
│   └── main
│       ├── java
│       │   └── com.example.accessmanagement
│       │       ├── SignUpServlet.java
│       │       ├── LoginServlet.java
│       │       ├── SoftwareServlet.java
│       │       ├── RequestServlet.java
│       │       └── ApprovalServlet.java
│       └── webapp
│           ├── WEB-INF
│           │   └── web.xml
│           ├── signup.jsp
│           ├── login.jsp
│           ├── createSoftware.jsp
│           ├── requestAccess.jsp
│           └── pendingRequests.jsp
└── README.md
```

## Installation and Setup

1. **Clone the Repository**
   ```bash
   git clone <repository_url>
   cd UserAccessManagementSystem
   ```

2. **Set Up PostgreSQL Database**
   - Ensure PostgreSQL is installed and running.
   - Create a new database and run the following SQL script to create the necessary tables:

     ```sql
     CREATE TABLE users (
         id SERIAL PRIMARY KEY,
         username TEXT UNIQUE NOT NULL,
         password TEXT NOT NULL,
         role TEXT CHECK (role IN ('Employee', 'Manager', 'Admin')) NOT NULL
     );

     CREATE TABLE software (
         id SERIAL PRIMARY KEY,
         name TEXT NOT NULL,
         description TEXT,
         access_levels TEXT CHECK (access_levels IN ('Read', 'Write', 'Admin')) NOT NULL
     );

     CREATE TABLE requests (
         id SERIAL PRIMARY KEY,
         user_id INTEGER REFERENCES users(id),
         software_id INTEGER REFERENCES software(id),
         access_type TEXT CHECK (access_type IN ('Read', 'Write', 'Admin')) NOT NULL,
         reason TEXT,
         status TEXT CHECK (status IN ('Pending', 'Approved', 'Rejected')) DEFAULT 'Pending'
     );
     ```

3. **Configure Database Connection**
   - Update the database connection details in each servlet file (e.g., `SignUpServlet.java`, `LoginServlet.java`, etc.):

     ```java
     String url = "jdbc:postgresql://localhost:5432/your_database_name";
     String user = "your_database_username";
     String password = "your_database_password";
     ```

4. **Deploy on Apache Tomcat**
   - Deploy the project on Apache Tomcat (version 9 or above).
   - Place the `.war` file in the Tomcat `webapps` directory or configure Tomcat to recognize your project directly from your IDE (Eclipse/IntelliJ).

5. **Run the Application**
   - Start Apache Tomcat and access the application at `http://localhost:8080/UserAccessManagementSystem`.

## Usage

1. **Sign-Up**: Access the registration page at `/signup.jsp`.
2. **Login**: Access the login page at `/login.jsp`.
3. **Role-Based Navigation**:
   - **Employee**: Access the request page at `/requestAccess.jsp`.
   - **Manager**: Access the pending requests page at `/pendingRequests.jsp`.
   - **Admin**: Access the software creation page at `/createSoftware.jsp`.

## Contributing

To contribute:
1. Fork the repository.
2. Create a new branch: `git checkout -b feature/your-feature-name`.
3. Commit your changes: `git commit -m 'Add some feature'`.
4. Push to the branch: `git push origin feature/your-feature-name`.
5. Open a pull request.
