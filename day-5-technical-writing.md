Exercise A: User Manual Procedure
Task: Creating and Activating a Python Virtual Environment and Installing a Package
1. Introduction
A Python virtual environment is an isolated workspace that allows developers to install and manage packages separately for each project. This prevents conflicts between package versions used by different projects.
This procedure explains how a beginner can create a virtual environment, activate it, install a Python package, and verify that the installation was successful using Windows PowerShell.
2. Prerequisites
Before starting, ensure that you have:
A computer running Windows 10 or Windows 11.
Python 3 installed on your computer.
Access to Windows PowerShell or the VS Code integrated terminal.
An active internet connection to download packages.
Basic knowledge of opening folders and running commands.
The pip package installer, which is normally included with Python.
3. Step-by-Step Procedure
Step 1: Open Windows PowerShell.
Press the Windows key, search for PowerShell, and open the application.
Expected result: A PowerShell terminal window appears.
Step 2: Create a project directory.
Run the following command:
mkdir my_python_project
Expected result: A new folder named my_python_project is created.
Step 3: Navigate into the project directory.
Run:
cd my_python_project
Expected result: The terminal is now working inside the project directory.
Step 4: Create a virtual environment.
Run:
python -m venv venv
Expected result: A new folder named venv is created inside the project directory. It contains the files needed to run an isolated Python environment.
Step 5: Activate the virtual environment.
Run:
.\venv\Scripts\Activate.ps1
Expected result: The word (venv) appears at the beginning of the terminal prompt, indicating that the environment is active.
Step 6: Install the requests package.
Run:
python -m pip install requests
Expected result: The requests package is downloaded and installed successfully.
Step 7: Verify the package installation.
Run:
python -m pip show requests
Expected result: Information about the installed requests package, including its version and installation location, is displayed.
Step 8: Deactivate the virtual environment.
Run:
deactivate
Expected result: The (venv) label disappears from the terminal prompt, indicating that the virtual environment is no longer active.
4. Screenshot Description
Screenshot 1: Successful virtual environment setup
The screenshot should show the Windows PowerShell terminal with the project directory, the activated (venv) environment, and the successful installation of the requests package.
The screenshot should also show the output of the pip show requests command to confirm that the package has been installed correctly.
5. Troubleshooting Note
Common problem: PowerShell does not allow script execution.
A beginner may encounter an error stating that script execution is disabled when attempting to activate the virtual environment.
Solution:
Open PowerShell and run:
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
Confirm if prompted, then activate the environment again:
.\venv\Scripts\Activate.ps1
This temporary setting applies only to the current PowerShell session.
6. Conclusion
A Python virtual environment helps developers manage project dependencies independently and avoid conflicts between package versions. By following these steps, beginners can create an isolated Python workspace, install packages, verify installations, and manage their development environments effectively.

Exercise B: API Reference Entry
API Documentation: Create a New Task
1. Endpoint Overview
Endpoint Name: Create a New Task
HTTP Method: POST
Endpoint Path: /api/v1/projects/{project_id}/tasks
Description:
This endpoint allows an authenticated user to create a new task within an existing project management application. The user provides a task title, an optional description, an assignee, a due date, and a priority level.
When the request is successful, the system creates the task, assigns it a unique task ID, and returns the newly created task details.
2. Authentication Requirements
Authentication is required to access this endpoint.
Authentication Method: Bearer Token
The user must include a valid access token in the Authorization header.
Example:
Authorization: Bearer YOUR_ACCESS_TOKEN
3. Request Headers
Header
Data Type
Required
Description
Authorization
String
Yes
Contains the user's valid Bearer access token.
Content-Type
String
Yes
Specifies that the request body is formatted as JSON.
Accept
String
No
Indicates that the client expects a JSON response.

Example:
Content-Type: application/json
Accept: application/json
Authorization: Bearer YOUR_ACCESS_TOKEN
4. Request Parameters
A. Path Parameters
Parameter
Data Type
Required
Description
project_id
Integer
Yes
The unique ID of the project where the task will be created.

Example:
/api/v1/projects/105/tasks
B. Query Parameters
This endpoint does not require query parameters.
C. Request Body Parameters
The request body must contain valid JSON data.
Parameter
Data Type
Required
Description
title
String
Yes
The name or title of the task.
description
String
No
Additional information explaining the task.
assignee_id
Integer
Yes
The unique ID of the user assigned to complete the task.
due_date
String (Date)
Yes
The deadline for completing the task, formatted as YYYY-MM-DD.
priority
String
Yes
The task priority. Accepted values are low, medium, or high.

5. Example Request
Request URL:
POST /api/v1/projects/105/tasks
Request Body:
{
  "title": "Prepare Project Progress Report",
  "description": "Prepare and submit the monthly project progress report.",
  "assignee_id": 24,
  "due_date": "2026-12-15",
  "priority": "high"
}
Explanation:
title: Identifies the task.
description: Provides additional task details.
assignee_id: Identifies the user responsible for the task.
due_date: Specifies the task deadline.
priority: Indicates the importance of the task.
6. Successful Response
HTTP Status Code: 201 Created
The server returns this response when the task has been successfully created.
Example Response Body:
{
  "success": true,
  "message": "Task created successfully.",
  "data": {
    "id": 501,
    "project_id": 105,
    "title": "Prepare Project Progress Report",
    "description": "Prepare and submit the monthly project progress report.",
    "assignee_id": 24,
    "due_date": "2026-12-15",
    "priority": "high",
    "status": "pending",
    "created_at": "2026-11-10T09:30:00Z"
  }
}
7. HTTP Response Codes
The endpoint may return the following HTTP status codes:
Status Code
Response
Explanation
201
Created
The task was successfully created.
400
Bad Request
The request contains invalid data or incorrectly formatted JSON.
401
Unauthorized
The authentication token is missing, invalid, or expired.
403
Forbidden
The authenticated user does not have permission to create tasks in the selected project.
404
Not Found
The specified project or assignee does not exist or cannot be accessed.
409
Conflict
The request conflicts with an existing resource or application rule.
415
Unsupported Media Type
The request does not use the supported JSON content type.
422
Unprocessable Entity
The request format is valid, but one or more fields fail validation, such as an invalid priority value or date.
429
Too Many Requests
The user has exceeded the allowed request limit.
500
Internal Server Error
An unexpected server-side problem prevented the task from being created.
503
Service Unavailable
The service is temporarily unavailable.

8. Important Validation Rules
The API should enforce the following rules before creating a task:
The task title must not be empty.
The description is optional.
The assignee ID must refer to an existing, eligible project user.
The due date must follow the YYYY-MM-DD format.
The priority must be either low, medium, or high.
The project must exist and the authenticated user must have permission to create tasks in it.
If validation fails, the API should return an appropriate error response explaining the problem.
9. Conclusion
The Create a New Task endpoint provides a structured way for authenticated users to add tasks to an existing project. The documentation identifies the endpoint, authentication requirements, request parameters, headers, sample JSON data, and possible HTTP response codes.
Providing complete API documentation helps developers understand how to integrate the endpoint correctly, reduces implementation errors, and makes application maintenance easier.

