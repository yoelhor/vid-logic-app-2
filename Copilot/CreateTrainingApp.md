# Instructions for the GitHub Copilot

Create a single page application within the index.html file, titled "Woodgrove online school." The application's design should reflect a professional online school user interface with just one course "customer data handling", utilizing a simple grayscale palette inspired by Bootstrap. Buttons and other UI elements are to retain Bootstrap’s default color scheme (use the primary color). For the JavaScript framework, implement jQuery. All JavaScript code should use jQuery.

The application has three key sections: “login”, “main” (home page), “issuance”. When the a user navigates to the app, it opens the "login" section, upon successfully sign-in, shows the "maim" section, and when a user completes the training shows the "“issuance”" section. All HTML element IDs, comments, and JavaScript functions must begin with “login”, “main” and “issuance”. All three sections should be centered and cover the entire screen.

## Login section

In the "login" section render a login form with username and password, and a login button. It's not a real login page and any credentials will take the user to the "main" section. 

## Main section

In the main page, generated a list of 10 online courses. One of them should be named "customer data handling". User can select the "customer data handling" training and start the course. There is not need to do the selection option for other courses.

The  "customer data handling" should show a short description and 4 steps to complete the course. At the bottom of the "customer data handling" page, shows the option to "receive credit". This receive credit button will take the user to the “issuance” section. 

## Issuance section

The "issuance" section includes a textbox for entering the display name, an option to upload a photo, and a button to submit the request. Selecting the “submit button” calls a JavaScript function named "StartIssuanceFlow".
The "StartIssuanceFlow" function begins, clearing resetting the UI including error message, and the notification area. Follow by creating a “state” parameter, using a uniquely generated GUID, which is retained in a global variable for subsequent reference. Generate a PIN code within the range of 1263 to 9858. Following this, a web API POST request is issued to the "issuance endpoint," accompanied by a JSON payload containing the "display name," "photo," ,”pin” and the “state” parameters. 
The API responds with a JSON object that includes a "url," intended to be rendered as a QR code for user scanning. Additionally, on success it invokes a function called CheckStatus


## Status section

The CheckStatus function should be called every 2 seconds for both the "issuance" and the "presentation" flows.
The CheckStatus function sends a POST request to the “status endpoint” with a JSON payload containing the "state" parameter. The “status endpoint” returns the user's current status, which should be presented to the user in the respective notification area. Furthermore, a circular progress indicator should visually display the flow's status, progressing from 0% to 100%.
Upon successful completion, check the “status” attribute and the type of the flow (issuance or presentation).
 
- For request_created set the progress to 35% and the message should be “Please scan the QR code with your mobile device”.
- request_retrieved set the progress to 60% for issuance the message should be “Please enter the PIN code on your mobile device”, and for “presentation” it should be “Please select the credentials to present on your mobile device”. Then hide the QR code area.
- issuance_successful set the progress to 100%, the message to “You successfully obtained your credential, please check your mobile device”. Then hide the PIN code area. 
- presentation_verified set the progress to 100%, the message to “Your credentials have been successfully verified”. Next, validate the “claims” attribute, then render all attributes as key-value pairs, omitting any keys with empty values.

## General

Use constants for all messages and the three endpoint URLs in the JavaScript and place them at the top of the JavaScript section.
Use the index.html file for both HTML, CSS and JavaScript code

