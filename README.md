### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- https://documenter.getpostman.com/view/28551494/2sA35Bc4n2
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  [git clone https://github.com/rashadkhan97/Automated-Testing-of-Rest-Booking-API-with-Newman-Report.git]
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   View the results in the Runner tab once the tests are complete.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
	//DYNAMIC CREATION LIST FOR ALL VARIABLES
	//First Name
	var firstname = pm.variables.replaceIn("{{$randomFirstName}}");
	pm.environment.set("firstname", firstname)
	
	//Last Name
	var lastname = pm.variables.replaceIn("{{$randomLastName}}");
	pm.environment.set("lastname", lastname); //calling enivorment to get lastname in enviroment
	
	
	//totalprice
	var totalprice = pm.variables.replaceIn("{{$randomInt}}");
	pm.environment.set("totalprice", totalprice)
	
	//depositpaid
	var depositpaid = pm.variables.replaceIn("{{$randomBoolean}}");
	pm.environment.set("depositpaid", depositpaid)
	
	//calling moment library for Checkin & Check out
	const moment = require("moment");       
	// moment is a library for date and time
	const today = moment();
	//for checking
	pm.environment.set("checkin", today.add(0,'d').format("YYYY-MM-DD"));
	pm.environment.set("checkout", today.add(5, 'd').format("YYYY-MM-DD"));
	
	//additional needs 
	var additionalneeds = pm.variables.replaceIn("{{$randomProduct}}");
	pm.environment.set("additionalneeds", additionalneeds)
	
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{totalPrice}},
	  "depositpaid" : {{depositPaid}},
	  "bookingdates" : {
    	  "checkin" : "{{checkin}}",
    	  "checkout" : "{{checkout}}"
	  },
	  "additionalneeds" : "{{additionalNeeds}}"
  }
```
  **Response Body:**
 ```console 
  {
    "bookingid": 1394,
    "booking": {
        "firstname": "Brianne",
        "lastname": "Jacobson",
        "totalprice": 605,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2024-03-25",
            "checkout": "2024-03-30"
        },
        "additionalneeds": "Pants"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Brianne",
    "lastname": "Jacobson",
    "totalprice": 605,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2024-03-25",
        "checkout": "2024-03-30"
    },
    "additionalneeds": "Pants"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "0d1b2ff4d291883"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
	//DYNAMIC CREATION LIST FOR ALL VARIABLES
	//First Name
	
	var updated_firstname = pm.variables.replaceIn("{{$randomFirstName}}");
	pm.environment.set("updated_firstname", updated_firstname)
	
	//Last Name
	var updated_lastname = pm.variables.replaceIn("{{$randomLastName}}");
	pm.environment.set("updated_lastname", updated_lastname); //calling enivorment to get lastname in enviroment
	
	
	//totalprice
	var updated_totalprice = pm.variables.replaceIn("{{$randomInt}}");
	pm.environment.set("updated_totalprice", updated_totalprice)
	
	//depositpaid
	var updated_depositpaid = pm.variables.replaceIn("{{$randomBoolean}}");
	pm.environment.set("updated_depositpaid", updated_depositpaid)
	
	//calling moment library for Checkin & Check out
	const moment = require("moment");       
	// moment is a library for date and time
	const today = moment();
	//for checking
	pm.environment.set("updated_checkin", today.add(1,'d').format("YYYY-MM-DD"));
	pm.environment.set("updated_checkout", today.add(5, 'd').format("YYYY-MM-DD"));
	
	//additional needs 
	var updated_additionalneeds = pm.variables.replaceIn("{{$randomProduct}}");
	pm.environment.set("updated_additionalneeds", updated_additionalneeds)
```
  **Request Body:** 
 ```console 
  {
	"firstname" : "{{updated_firstname}}",
	"lastname" : "{{updated_lastname}}",
	"totalprice" : "{{updated_totalprice}}",
	"depositpaid" : {{updated_depositpaid}},
	"bookingdates" : {
    	"checkin" : "{{updated_checkin}}",
    	"checkout" : "{{updated_checkout}}"
	},
	"additionalneeds" : "{{updated_additionalneeds}}"
}
```
  **Response Body:**
 ```console 
  {
    "firstname": "Justen",
    "lastname": "Marvin",
    "totalprice": 620,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-03-26",
        "checkout": "2024-03-31"
    },
    "additionalneeds": "Bike"
}
```

 ## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run Rashadul_Islam_SQA_API_Testing.postman_collection.json -e Rashadul_Islam_SQA_API_Testing.postman_environment.json
```
- Run Command for Report: 
```console 
newman run Rashadul_Islam_SQA_API_Testing.postman_collection.json -e Rashadul_Islam_SQA_API_Testing.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:
![image](https://github.com/rashadkhan97/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/76771109/65e61407-2871-4ff8-a4db-75b13410c380)
![image](https://github.com/rashadkhan97/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/76771109/94a17809-c1f9-41fd-971d-3369e57d894a)
![image](https://github.com/rashadkhan97/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/76771109/40a5417b-78cf-40e5-b62e-32812f4615cf)
![image](https://github.com/rashadkhan97/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/76771109/49802988-8631-4832-8dc8-b4c1a3431909)
![image](https://github.com/rashadkhan97/Automated-Testing-of-Rest-Booking-API-with-Newman-Report/assets/76771109/3045a1c7-db19-44da-bf32-33a9082abab4)









