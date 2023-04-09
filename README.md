# SoftUni-JS-Application-Exam

This is SPA with page and lit-html.

Application Requirements
Navigation Bar (5 pts)
Implement a NavBar for the app: 
Navigation links should correctly change the current page (view). All users can see the site logo that should be a link to the Home page as well as the Dashboard which should link to the Fruits page. Guests (un-authenticated visitors) can see the links to the Login and Register and Search pages. The logged-in user navbar should contain the links to the Add Fruit, Search pages and a link for the Logout action.
Logged-in User navigation example:



Guest navigation example: 


Home Page (10 pts)
Implement a static Home page for the app using the structure for it from the given resources. 

Logged-in Page (5 pts)
The included REST service comes with the following premade user accounts, which you may use for development:
{ "email": "peter@abv.bg", "password": "123456" }
{ "email": "john@abv.bg", "password": "123456" }
The Login page contains a form for existing user authentication. By providing an email and password the app should log a user in the system if there are no empty fields.

Send the following request to perform login:
Method: POST
URL: /users/login
The required headers are described in the documentation. The service expects a body with the following shape:
{
  email,
  password
}
Upon success, the REST service will return the newly created object with an automatically generated _id and a property accessToken, which contains the session token for the user – you need to store this information using sessionStorage or localStorage, in order to be able to perform authenticated requests.
If the login was successful, redirect the user to the Home page. If there is an error, or the validations don’t pass, display an appropriate error message, using a system dialog (window.alert).
Register User (10 pts)
By given email, password app should register a new user in the system. All fields are required – if any of them is empty, or the password and repeat password doesn't match, display an error.

Send the following request to perform registration:
Method: POST
URL: /users/register
Required headers are described in the documentation. The service expects a body with the following shape:
{
  email,
  password
}
Upon success, the REST service will return the newly created object with an automatically generated _id and a property accessToken, which contains the session token for the user – you need to store this information using sessionStorage or localStorage, in order to be able to perform authenticated requests.
If the registration was successful, redirect the user to the Home page. If there is an error, or the validations don’t pass, display an appropriate error message, using a system dialog (window.alert).
Logout (5 pts)
The logout action is available to logged-in users. Send the following request to perform logout:
Method: GET 
URL: /users/logout
The required headers are described in the documentation. Upon success, the REST service will return an empty response. Clear any session information you’ve stored in browser storage.
If the logout was successful, redirect the user to the Home page.
Dashboard (15 pts)
This page displays a list of all fruits in the system. Clicking on the More Info button in the fruit card leads to the details page for the selected fruit. This page should be visible to guests and logged-in users.

If there are no fruits, the following view should be displayed:

Send the following request to read the list of records:
Method: GET
URL: /data/fruits?sortBy=_createdOn%20desc
The required headers are described in the documentation. The service will return an array of fruits.
Adding a New Fruit Record(15 pts)
The Create page is available to logged-in users. It contains a form for adding a new fruit. Check if all the fields are filled before you send the request.

To create fruit, send the following request:
Method: POST
URL: /data/fruits
The required headers are described in the documentation. The service expects a body with the following shape:
{
  name,
  imageUrl, 
  description, 
  nutrition
} 
The required headers are described in the documentation. The service will return the newly created record. Upon success, redirect the user to the Fruit page.
Fruit Details (10 pts)
All users should be able to view details about fruits. Clicking the More Info button in a fruit card should display the Details page. If the currently logged-in user is the creator, the Edit and Delete buttons should be displayed. Otherwise they should not be available. The view should look like this to the creator of the fruit record:

The view for guests should look like:

Send the following request to read a single fruit:
Method: GET
URL: /data/fruits/:id
Where :id is the ID of the desired card. The required headers are described in the documentation. The service will return a single object.
Editing a Fruit Record (15 pts)
The Edit page is available to logged-in users and it allows authors to edit their own fruits. Clicking the Edit link of a particular fruit on the Details page should display the Edit page, with all fields filled with the data for the fruit. It contains a form with input fields for all relevant properties. Check if all the fields are filled before you send the request. 
 
To edit a fruit record, send the following request:
Method: PUT
URL: /data/fruits/:id
Where :id is the id of the desired card.
The service expects a body with the following shape:
{
  name,
  imageUrl, 
  description, 
  nutrition
} 
Required headers are described in the documentation. The service will return the modified record. Note that PUT requests do not merge properties and will instead replace the entire record. Upon success, redirect the user to the Details page for the current fruit.
Delete a Fruit Record (10 pts)
The delete action is available to logged-in users, for fruit records they have created. When the author clicks on the Delete action on any of their fruit, a confirmation dialog should be displayed, and upon confirming this dialog, the record should be deleted from the system.
To delete fruit record, send the following request:
Method: DELETE
URL: /data/fruits/:id
Where :id is the id of the desired fruit. Required headers are described in the documentation. The service will return an object, containing the deletion time. Upon success, redirect the user to the Fruits page.
(BONUS) Search Page (15 pts)
The Search page allows both logged-in users and guests to filter fruits by their name. It contains an input field and, upon submitting a query, a list of all matching fruits. Check if the field is filled before you send the request. If it isn't filled show an alert message.

If you find some fruit records, the following view should be displayed:

If you find fruit, the following view should be displayed:


Send the following request to read a filtered list of fruits by their name:
Method: GET
URL: /data/fruits?where=name%20LIKE%20%22${query}%22
Where {query} is the search query that the user has entered in the input field. Required headers are described in the documentation. The service will return an array of fruits.
Subtmitting Your Solution
Place in a ZIP file your project folder. Exclude the node_modules folder. Upload the archive to Judge.
 
 
It will take several minutes for Judge to process your solution!

Appendix A: Using the Local REST Service
Starting the Service
The REST service will be in a folder named “server” inside the provided resources archive. It has no dependencies and can be started by opening a terminal in its directory and executing:
node server.js
If everything is initialized correctly, you should see a message about the host address and port on which the service will respond to requests.
Sending Requests
To send a request, use the hostname and port, shown in the initialization log and resource address and method as described in the application requirements. If data needs to be included in the request, it must be JSON-encoded, and the appropriate Content-Type header must be added. Similarly, if the service is to return data, it will be JSON-encoded. Note that some requests do not return a body and attempting to parse them will throw an exception.
Read requests, as well as login and register requests do not require authentication. All other requests must be authenticated.
Required Headers
To send data to the server, include a Content-Type header and encode the body as a JSON-string:
Content-Type: application/json
{JSON-encoded request body as described in the application requirements}
To perform an authenticated request, include an X-Authorization header, set to the value of the session token, returned by an earlier login or register request:
X-Authorization: {session token}
Server Response
Data response:
HTTP/1.1 200 OK
Access-Contrl-Allow-Origin: *
Content-Type: application/json
{JSON-encoded response data}
Empty response:
HTTP/1.1 204 No Content
Access-Contrl-Allow-Origin: *
Error response:
HTTP/1.1 400 Request Error
Access-Contrl-Allow-Origin: *
Content-Type: application/json
{JSON-encoded error message}
