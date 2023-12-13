## API TEST PLAN

#### Test categories:

- Consumer app endpoints

- Driver app endpoints

- Touchscreen endpoints
  
  This test plan covers all endpoints which cover whole functionality of our application.
  
  These are separated into three major groups:
  
  - Locations API (parcel lockers/cabinets)
  
  - Parcels API (send/receive/update statuses, all connected with parcel functionality)
  
  - Users API (login/signup/signout/user info endpoints)
    
    We will test all groups accordingly in Postman with Tests Generation feature.
    
    ### Environment Variables:
    
    - `BACKEND_HOSTNAME`: [https://shiply-server.onrender.com](https://shiply-server.onrender.com)
    - `DEV_HOSTNAME`: http://localhost/3000

### Locations API endpoints

#### Date: 5.12

#### Test 1: Get Locations

- **Pass/Fail Requirement:** Response status code should be 200.
- **Description:** Retrieve all locations using the "Get Locations" endpoint.
- **Expected Result:** The response status code is 200, and the response contains a JSON array of locations, each having a valid ID, title, and non-empty address.

#### Test 2: Reserve Random Cabinet

- **Pass/Fail Requirement:** Response status code should be 200, and the reservation should be successful.
- **Description:** Attempt to reserve a random cabinet using the "Reserve Random Cabinet" endpoint.
- **Expected Result:** The response status code is 200, and the response JSON includes a success message, location ID, and cabinet ID. The location and cabinet IDs should be positive integers.

#### Test 3: Reserve Empty Cabinet

- **Pass/Fail Requirement:** Response status code should be 200, and the reservation should be successful.
- **Description:** Attempt to reserve an empty cabinet using the "Reserve Empty Cabinet" endpoint.
- **Expected Result:** The response status code is 200, and the response JSON includes a success message, location ID, and cabinet ID. The location and cabinet IDs should be positive integers.

#### Test 4: Get All Cabinets by Location ID

- **Pass/Fail Requirement:** Response status code should be 200.
- **Description:** Retrieve all cabinets for a specific location using the "Get All Cabinets by Location ID" endpoint.
- **Expected Result:** The response status code is 200, and the response contains a JSON array of cabinets. Each cabinet should have a non-empty number, status, and a non-negative location ID.

#### Test 5: Update Cabinet Status

- **Pass/Fail Requirement:** Response status code should be 200, and the cabinet status should be successfully updated.
- **Description:** Attempt to update the status of a specific cabinet using the "Update Cabinet Status" endpoint.
- **Expected Result:** The response status code is 200, and the response JSON includes a success message. The "message" field is a non-empty string, and the updated status should be one of the following: 'created', 'sent', 'picked', 'delivered', or 'received'.

---

## Parcel APIs

### 1. **Get all parcels**

- **Date:** 3.12.23
- **Pass/Fail Requirement:**
  - The response status code should be 200.
  - The response is an array with at least one element.
  - Parcel ID is a non-negative integer.
  - Receiver ID is a non-negative integer.
  - Driver ID is a non-negative integer.
- **Description of Test:**
  - Send a GET request to `https://shiply-server.onrender.com/api/parcels/getAllParcels`.
  - Check if the response status code is 200.
  - Verify that the response is an array with at least one element.
  - Ensure that Parcel ID, Receiver ID, and Driver ID in each parcel are non-negative integers.
- **Expected Result:** All test cases should pass.

### 2. **Get Parcels by ID Endpoint**

- **Date:** 3.12.23
- **Pass/Fail Requirement:**
  - The response status code should be 200.
  - ParcelID is a non-negative number.
- **Description of Test:**
  - Send a GET request to `https://shiply-server.onrender.com/api/parcels/11`.
  - Check if the response status code is 200.
  - Verify that ParcelID in each parcel is a non-negative number.
- **Expected Result:** All test cases should pass.

### 3. **Create Parcel **

- **Date:** 3.12.23
- **Pass/Fail Requirement:**
  - The response status code should be 200.
  - Response has the required fields: success, trackingNumber, pinCode, status, receiverName, receiverEmailAddress, senderDropOffLocation.
  - Tracking number is a non-empty string.
  - Pin code is a non-empty string.
  - Email address is in a valid format.
- **Description of Test:**
  - Send a POST request to `https://shiply-server.onrender.com/api/parcels/createParcel` with the provided payload.
  - Check if the response status code is 200.
  - Verify that the required fields are present in the response.
  - Check that tracking number and pin code are non-empty strings.
  - Ensure that the receiver's email address is in a valid format.
- **Expected Result:** All test cases should pass.

### 4. **Get parcels by receiver email **

- **Date:** 3.12
- **Pass/Fail Requirement:**
  - The response status code should be 200.
  - The 'status' field is a non-empty string.
- **Description of Test:**
  - Send a POST request to `https://shiply-server.onrender.com/api/parcels/receiver/getParcels` with the provided payload.
  - Check if the response status code is 200.
  - Verify that the 'status' field in each parcel is a non-empty string.
- **Expected Result:** All test cases should pass.

### 5. **Track Parcel**

- **Date:** 3.12
- **Pass/Fail Requirement:**
  - The response status code should be 200.
  - Response content type is application/json.
  - Response is an array with at least one element.
  - Tracking number is a non-empty string.
- **Description of Test:**
  - Send a GET request to `http://localhost/3000/api/parcels/trackParcel/64859535/`.
  - Check if the response status code is 200.
  - Verify that the response content type is application/json.
  - Ensure that the response is an array with at least one element.
  - Check that the tracking number in each parcel is a non-empty string.
- **Expected Result:** All test cases should pass.

### Postman Collection Link:

- [Parcels APIs Postman Collection](https://www.postman.com/martian-sunset-211991/workspace/shiply/collection/30971036-738f77ec-2754-4ba2-9e30-792e1fc03bcd?action=share&source=collection_link&creator=30971036)

#### Users API

#### 1. Login user

Certainly, here is a summary of the "Users API" documentation you provided:

### Users API Documentation

#### General Information

- **Postman Collection:** [Users API Collection](https://www.postman.com/martian-sunset-211991/workspace/shiply/collection/30971036-a79341ee-61d0-46a0-8718-fa4ed996f715?action=share&source=collection_link&creator=30971036)

#### Endpoints

1. **Login User**
   
   - **Endpoint:** `POST /api/auth/login`
   
   - **Description:** Login user with idToken from Firebase.
   
   - **Request:**
     
     - Method: `POST`
     - Headers:
       - Content-Type: application/json
     - Body (Raw JSON):
       
       ```json
       {
         "idToken": "YOUR_FIREBASE_ID_TOKEN"
       }
       ```
   
   - **Tests:**
     
     - Response status code should be 401.
     - Response should have required fields: clientId, clientInfo, clientEmail, FirebaseID.
     - `clientEmail` should be in a valid email format.
     - Client information fields should be null or empty.
     - Verify the presence and non-emptiness of the 'error' field in the response.
   
   - **Response:**
     
     - Status: OK (200)
     - Body:
       
       ```json
       [
         {
           "clientId": 10,
           "clientInfo": "boba me1",
           "clientName": null,
           "clientEmail": "boba1@gmail.com",
           "clientPhone": null,
           "clientAddress": null,
           "clientAccountStatus": null,
           "FirebaseID": "YOUR_FIREBASE_ID"
         }
       ]
       ```

2. **Sign Up User**
   
   - **Endpoint:** `POST /api/auth/signup`
   - **Description:** Sign up a new user.
   - **Request:**
     - Method: `POST`
     - Headers:
       - Content-Type: application/json
     - Body (Raw JSON):
       
       ```json
       {
         "idToken": "YOUR_FIREBASE_ID_TOKEN",
         "email": "boba@gmail.com",
         "displayName": "(name of user)",
         "clientAddress": "Ziliboba street 2"
       }
       ```
   - **Response:**
     - Status: OK (200)




