

---

# Bike Service Application

This project is a bike service application that allows bike service station owners and customers to manage bike services, bookings, and queries. The application includes separate dashboards for owners and customers, and integrates Twilio for OTP verification.


Visit the website: <a href="https://bikeservice-omega.vercel.app/" style="font-size:40rem;">Bike Service Website</a>

When you visite this website follow this two steps:

   - First, **Login as an owner** and add the necessary service details provided at the bottom. For more details, please refer to the **owner flow**.
   - Next **Login as a customer** to view all services in that city's service station and below workflow.

# NOTE : Login with provided email and password in  Setting Up Twilio for OTP
   - When you log in as a customer and  click the **Book Now** button. It will show the OTP box to enter the OTP sent to your mobile number. For that, you need to add your mobile number in the Twilio website for OTP generation. So follow **step 9 in Setting Up Twilio for OTP**.

**click the add caller ID  button**
<p align="center">
  <img src="https://github.com/user-attachments/assets/b899aa49-033e-4b26-91c2-fcfc52bd48e8" alt="Image" style="width: 700px;"/>
</p>

 **verify customer mobile number that  your are registered and then mobile number get add in it and you will recieve OTP.**

<p align="center">
  <img src="https://github.com/user-attachments/assets/3540add0-baf9-4a8b-9386-2a7fc313855a" alt="Image" style="width: 700px;"/>
</p>


# Installation: 
  To run the project, install  [Node js](https://nodejs.org/en/download/package-manager/current) and [MongoDB Compass](https://www.mongodb.com/try/download/compass).

  Download the project and run each frontend and backend in separate terminals with 
  
  ```bash
npm start
```
  
  Before running the **backend folder with npm start**  . 
  
  please install express using  
  ``` bash
npm install express
```

## Project Flow

### 1. User Roles

- **Owner** (for bike service station)
- **Customer/User** (to book the service)

### 2. Owners

There are two owners with different service stations:

- **Owner 1:**
  - Email: kavinbr.20msc@kongu.edu
  - Password: MSC@KONUG
  - City: Erode

- **Owner 2:**
  - Email: yokeshr.20msc@kongu.edu
  - Password: Dhivya753@
  - City: Gobi

You can add more owners in the `Login.jsx` file in the owners array.


### 3. Database Schemas

- **User**
- **Service**
- **Booking**
- **Contact**


**User Schema**
```
{
  "_id": "ObjectId",
  "email": "String (required, unique)",
  "mobileNumber": "String (required, unique)",
  "password": "String (required)",
  "__v": "Number"
}

Sample Data

{
  "_id": "668c05c988c9e248dbab497b",
  "email": "vimalraja@gmail.com",
  "mobileNumber": "9487557658",
  "password": "$2a$10$cypkw3gYTT4JfnYTlxd/R.A0B4Ce2w4ZlXaA0VtJIBuzjlmJPZc/y",
  "__v": 0
}
```



**Service Schema**
```
{
  "_id": "ObjectId",
  "name": "String (required)",
  "description": "String (required)",
  "cost": "Number (required)",
  "duration": "Number (required)",
  "image": "String (required)",
  "city": "String (required)",
  "ownerEmail": "String (required)",
  "__v": "Number"
}

Sample Data

{
  "_id": "668c127288c9e248dbab49cf",
  "name": "General service check-up",
  "description": "Ensure your bike stays in top condition with our thorough check-up.",
  "cost": 7000,
  "duration": 10,
  "image": "backend/uploads/1720455794230.jpg",
  "city": "erode",
  "ownerEmail": "kavinbr.20msc@kongu.edu",
  "__v": 0
}
```

**Booking Schema**

```
{
  "_id": "ObjectId",
  "userName": "String (required)",
  "userId": "ObjectId (ref: 'User', required)",
  "service": "ObjectId (ref: 'Service', required)",
  "email": "String (required)",
  "serviceName": "String (required)",
  "mobileNumber": "String (required)",
  "bikeBrand": "String (required)",
  "bikeModel": "String (required)",
  "bikeNumber": "String (required)",
  "address": "String (required)",
  "serviceDate": "Date (required)",
  "problemDetails": "String (required)",
  "emailMessage": "String (required)",
  "ownerEmail": "String (required)",
  "city": "String (required)",
  "status": "String (enum: ['pending', 'accepted', 'rejected', 'ready', 'completed'], default: 'pending')",
  "__v": "Number"
}

Sample Data

{
  "_id": "668be3e196eb7732956b0e60",
  "userName": "kavin",
  "userId": "66890d9baaed2112e80eafae",
  "email": "brkavin15@gmail.com",
  "serviceName": "gear clean",
  "mobileNumber": "9487557658",
  "bikeBrand": "TVS",
  "bikeModel": "Hero Xtreme 125R",
  "bikeNumber": "TN 36 AT1135",
  "address": "erode",
  "serviceDate": "2024-07-09T00:00:00.000Z",
  "problemDetails": "gear clean",
  "emailMessage": "Booking for service: gear clean on 2024-07-09",
  "ownerEmail": "kavinbr.20msc@kongu.edu",
  "city": "erode",
  "status": "completed",
  "__v": 0
}
```

**Contact Schema**

```
{
  "_id": "ObjectId",
  "userEmail": "String (required)",
  "message": "String (required)",
  "createdAt": "Date (default: Date.now)",
  "city": "String (required)",
  "ownerEmail": "String (required)",
  "__v": "Number"
}


Smaple Data

{
  "_id": "668d569995f448ba11c8e7f5",
  "userEmail": "brkavin15@gmail.com",
  "message": "good job",
  "city": "erode",
  "ownerEmail": "kavinbr.20msc@kongu.edu",
  "createdAt": "2024-07-09T15:26:17.649Z",
  "__v": 0
}
```

---
### 4. Customer Flow

- Customers need to register if they don't have an account, or log in if they do.
- Customers can view their profile and bookings.
- After logging in, customers can see the services available at their city's workstation.
- Customers can send messages or queries through the contact us footer.
- Clicking "View Details" on a service redirects to the `ServiceDetails` page.
- On the `ServiceDetails` page, customers can see complete details of the service and click "Book Now," which prompts OTP verification sent to their registered mobile number.
- OTP is sent via Twilio. Follow these steps to set up Twilio:


## Setting Up Twilio for OTP

1. Go to [Twilio](https://www.twilio.com/en-us).
   - Login with:
     
     - **Email:** naveenkumars.20msc@kongu.edu
     - **Password:** Naveenkumars@1510
       
     If it ask code  then click try another method and enter the below recovery code.
   
     - **Recovery code:** MN28TLEX6KQK6X3JQ5JKGCAB
       
   - Then go to step 8 and 9 directly or follow all steps below if you need to create a new account.

2. Click "Products" and choose "Verify," then click "START FOR FREE."
3. Sign up or continue with Google.
4. Enter the code sent to your sign-up email.
5. Enter your mobile number and the code sent to your mobile number.
6. Save the recovery code and click "Continue."
7. Create a new account with the following details:
   - **Account friendly name:** (any name)
   - **What will this account be used for?:** Twilio
   - **Mobile number and verification code**
   - Answer the questions:
     1. Identity & Verification (OTP & 2FA)
     2. Verify
     3. Sole proprietor / Self-employed
     4. With code
     5. Javascript
     6. No
8. In the copy below three values and add in `.env` file:
   - **Account SID**
   - **Auth Token**
   - **Twilio phone number**

9. **Add the customer's mobile number in "Verified Caller ID" in Twilio:**
   - Go to [Twilio Console](https://www.twilio.com/console).
   - Click on "Phone Numbers" link in the sidebar.
   - Click "Manage" under your Twilio phone number.
   - Click "Verified Caller IDs."
   - Add new caller ID of the customer number in Twilio.

### Using the OTP in Your Application:

- After entering the OTP, it verifies and redirects to the `BookService` page.
- Fill out the form and book the service.
- Customers receive an email from the owner and can view bookings on the homepage.

---


### 5. Owner Flow

- Owners do not need to register as their details are stored in the `Login.jsx` file.
- Log in as owner with email, password, and city.
- Owners are redirected to their dashboard after successful login.
- In the dashboard, owners can add services, view services, view bookings, and view messages for their city's service station.

#### Adding Services

Owners can add services provided in their city. When a customer books a service, the owner receives an email about the booking with status updates (pending, accepted, rejected, ready, completed).

- Owners can accept or reject bookings, and an email is sent to the customer with the status.
- When ready to deliver the bike, the booking status is updated to "Ready for Delivery" and an email is sent to the customer.
- After delivering the bike, the status changes to "Completed."
- Owners can log out after managing their services.

## Note

To send and receive emails between owners and customers, make sure to enable [Less Secure Apps in Gmail](https://myaccount.google.com/u/0/lesssecureapps) on owner email.
![image](https://github.com/user-attachments/assets/2fcf21d2-6626-4412-a233-45f907b4e789)


## Service Content

### 1. Oil Change

**Description:**
Keep your bike running smoothly and efficiently with our Comprehensive Bike Oil Change service. Regular oil changes are crucial for maintaining your bike’s engine performance and longevity. Our expert technicians will ensure that your bike receives the best care with high-quality engine oil specifically designed for your bike’s make and model.

**What Included:**
- Premium Engine Oil: We use top-grade engine oil to provide optimal lubrication, reduce friction, and enhance the overall performance of your bike’s engine.
- Oil Filter Replacement: We replace the old oil filter with a new one to ensure the engine oil stays clean and effective for longer periods.
- Engine Health Check: Our technicians perform a thorough inspection of your bike’s engine components to identify any potential issues early on.
- Drain and Refill: We carefully drain the old oil and refill it with fresh, premium-grade engine oil to keep your bike running smoothly.
- Environmental Disposal: We responsibly dispose of the used oil and filters in an environmentally friendly manner.

### 2. General Service Check-Up

**Description:**
Ensure your bike stays in top condition with our thorough General Service Check-Up. Regular maintenance is essential for the safety and longevity of your bike. Our experienced technicians will perform a comprehensive inspection and tune-up to keep your bike running smoothly and efficiently.

**What Included:**
- Complete Bike Inspection: Our technicians will conduct a detailed examination of your bike, checking all vital components for wear and tear, ensuring everything is in good working order.
- Brake System Check: We inspect and adjust the brake system, ensuring optimal performance and safety. This includes checking brake pads, cables, and fluid levels.
- Chain and Sprocket Maintenance: We clean, lubricate, and adjust the chain and sprockets to ensure smooth and efficient power transfer.
- Tire and Wheel Check: We inspect the tires for wear and tear, check tire pressure, and ensure wheels are properly aligned and balanced for a safe and smooth ride.
- Battery Check: We test the battery’s condition, ensuring it holds a charge and operates efficiently. This includes checking the terminals and connections.
- Air Filter Cleaning: We clean or replace the air filter to ensure your engine breathes clean air, improving performance and fuel efficiency.

### 3. Water Wash

**Description:**
Keep your bike looking pristine and running smoothly with our professional Water Wash service. Regular cleaning is essential to maintain your bike’s appearance and performance. Our skilled technicians will thoroughly clean your bike, ensuring it stays in top condition and free from dirt, grime, and debris.

**What Included:**
- Complete Bike Cleaning: Our technicians perform a thorough cleaning of your bike, removing dirt, grime, and debris from all surfaces to restore its original shine.
- High-Pressure Water Wash: We use high-pressure water jets to effectively clean hard-to-reach areas, ensuring every part of your bike is spotless.
- Engine Cleaning: We clean the exterior of the engine, removing dirt and grime that can affect performance and appearance.
- Seat and Handlebar Cleaning: We clean the seat and handlebars, ensuring they are free from dust and dirt for a comfortable and pleasant riding experience.
- Drying and Polishing: After washing, we thoroughly dry your bike and apply polish to enhance its shine and protect the paintwork from environmental elements.
- Inspection for Damage: During the cleaning process, our technicians inspect your bike for any signs of damage or wear, alerting you to any issues that may need attention.

---


