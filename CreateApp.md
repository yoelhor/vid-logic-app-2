# Instructions for the GitHub Copilot

Create a single page application within the index.html file, titled "Verified ID Sample." The application's design should reflect a professional helpdesk user interface, utilising a simple grayscale palette inspired by Bootstrap. Buttons and other UI elements are to retain Bootstrap’s default color scheme (use the primary color). For the JavaScript framework, implement jQuery.
Include a dark header section featuring navigation links for "Obtain Credential" and "Preset Credentials." Additionally, provide a link to the GitHub repository at https://github.com/yoelhor/vid-logic-app-2 (accompanied by the GitHub icon), and a privacy policy link at https://github.com/yoelhor/vid-logic-app-2/privacy (with an appropriate icon).
The application has three key scenarios: “main” (home page), “issuance”, and “presentation”. All HTML element IDs, comments, and JavaScript functions must begin with “main”, “issuance”, or “presentation”. All three sections should be centered and cover the entire screen (except the header).

## Main section

In the "main" section, users should be presented with two options: on the left, the option to "obtain" a credential, and on the right, the option to "present" their credentials. When a user selects either the obtain or present buttons—whether from the header or from the main section page—the corresponding JavaScript function, "render Issuance UI" or "render Presentation UI," should be invoked.
Both rendertIssuanceUI and renderPresentationUI navigate users to their respective UI components: "issuance" or "presentation." Each component should include a title, a close button that returns to the main section, “content area”, an “error area”, a “user notification area”, and a “submit button” triggering a JavaScript function. The notification area includes a circle that displays the progress of the flow, ranging from 0 to 100%, along with a simple text description of the status.

## Issuance section

The "issuance" section includes a textbox for entering the display name, an option to upload a photo, and a button to submit the request. Selecting the “submit button” calls a JavaScript function named "StartIssuanceFlow".
The "StartIssuanceFlow" function begins, clearing resetting the UI including error message, and the notification area. Follow by creating a “state” parameter, using a uniquely generated GUID, which is retained in a global variable for subsequent reference. Generate a PIN code within the range of 1263 to 9858. Following this, a web API POST request is issued to the "issuance endpoint," accompanied by a JSON payload containing the "display name," "photo," ,”pin” and the “state” parameters. 
The API responds with a JSON object that includes a "url," intended to be rendered as a QR code for user scanning. Additionally, on success it invokes a function called CheckStatus

## Presentation section

The "presentation" section includes a submit the request. Selecting the “submit button” calls a JavaScript function named "StartPresentationFlow".

The "StartPresentationFlow" function begins, clearing resetting the UI including error message, and the notification area. Follow by creating a “state” parameter, using a uniquely generated GUID, which is retained in a global variable for subsequent reference. Following this, a web API POST request is issued to the "presentation endpoint," accompanied by a JSON payload containing the “state” parameter. 
The API responds with a JSON object that includes a "url," intended to be rendered as a QR code for user scanning. Additionally, on success it invokes a function called CheckStatus.

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

