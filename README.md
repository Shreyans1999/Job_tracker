To implement the backend for the Job Application Tracker, here’s an API design along with documentation for each of the core features.

### API Design for Job Application Tracker

---

# Job Application Tracker API Design

## **1. User Authentication and Profiles**

### **Endpoints**

#### **1.1 User Registration**
**POST** `/api/auth/register`
- **Description**: Allows users to register an account.
- **Request Body**:
```json
{
  "name": "Shreyans Saklecha",
  "email": "saklechashreyans1999@gmail.com",
  "password": "securepassword123"
}
```
- **Response**:
```json
{
  "message": "User registered successfully",
  "user": {
    "id": 1,
    "name": "Shreyans Saklecha",
    "email": "saklechashreyans1999@gmail.com"
  }
}
```
- **Authentication**: Not required.

#### **1.2 User Login**
**POST** `/api/auth/login`
- **Description**: Logs in a user and returns a JWT.
- **Request Body**:
```json
{
  "email": "saklechashreyans1999@gmail.com",
  "password": "securepassword123"
}
```
- **Response**:
```json
{
  "token": "jwt-token-here",
  "user": {
    "id": 1,
    "name": "Shreyans Saklecha",
    "email": "saklechashreyans1999@gmail.com"
  }
}
```
- **Authentication**: Not required.

#### **1.3 Profile Management**
**PUT** `/api/users/profile`
- **Description**: Updates user profile information.
- **Request Body**:
```json
{
  "name": "Shreyans Saklecha",
  "careerGoals": "Aiming for a senior software engineering role"
}
```
- **Response**:
```json
{
  "message": "Profile updated successfully",
  "profile": {
    "name": "Shreyans Saklecha",
    "careerGoals": "Aiming for a senior software engineering role"
  }
}
```
- **Authentication**: Required.

---

## **2. Job Application Logging**

### **Endpoints**

#### **2.1 Log a Job Application**
**POST** `/api/applications`
- **Description**: Logs a new job application.
- **Request Body**:
```json
{
  "companyName": "InnovateTech",
  "jobTitle": "Full Stack Developer",
  "applicationDate": "2024-12-22",
  "status": "Applied",
  "notes": "Applied through the company website."
}
```
- **Response**:
```json
{
  "message": "Job application logged successfully",
  "application": {
    "id": 1,
    "companyName": "InnovateTech",
    "jobTitle": "Full Stack Developer",
    "status": "Applied"
  }
}
```
- **Authentication**: Required.

#### **2.2 Upload Attachments**
**POST** `/api/applications/:id/attachments`
- **Description**: Uploads documents like resumes and cover letters.
- **Request Body**: Form-data with files.
- **Response**:
```json
{
  "message": "Attachment uploaded successfully",
  "attachmentUrl": "https://s3.amazonaws.com/attachments/resume.pdf"
}
```
- **Authentication**: Required.

#### **2.3 Update Job Application**
**PUT** `/api/applications/:id`
- **Description**: Updates an existing job application.
- **Request Body**:
```json
{
  "status": "Interviewed",
  "notes": "Completed technical interview."
}
```
- **Response**:
```json
{
  "message": "Application updated successfully",
  "application": {
    "status": "Interviewed",
    "notes": "Completed technical interview."
  }
}
```
- **Authentication**: Required.

---

## **3. Reminder System**

### **Endpoints**

#### **3.1 Set a Reminder**
**POST** `/api/reminders`
- **Description**: Creates a follow-up reminder.
- **Request Body**:
```json
{
  "applicationId": 1,
  "reminderDate": "2024-12-29",
  "message": "Send a thank-you email to the recruiter"
}
```
- **Response**:
```json
{
  "message": "Reminder created successfully",
  "reminder": {
    "id": 1,
    "reminderDate": "2024-12-29",
    "message": "Send a thank-you email to the recruiter"
  }
}
```
- **Authentication**: Required.

#### **3.2 Get Upcoming Reminders**
**GET** `/api/reminders`
- **Description**: Retrieves all upcoming reminders.
- **Response**:
```json
[
  {
    "id": 1,
    "applicationId": 1,
    "reminderDate": "2024-12-29",
    "message": "Send a thank-you email to the recruiter"
  }
]
```
- **Authentication**: Required.

---

## **4. Company Information Management**

### **Endpoints**

#### **4.1 Store Company Information**
**POST** `/api/companies`
- **Description**: Adds a new company profile.
- **Request Body**:
```json
{
  "name": "InnovateTech",
  "industry": "Software Development",
  "size": "100-500",
  "notes": "Innovative company with a focus on AI."
}
```
- **Response**:
```json
{
  "message": "Company profile created successfully",
  "company": {
    "id": 1,
    "name": "InnovateTech"
  }
}
```
- **Authentication**: Required.

---

## **5. Application Progress Visualization**

### **Endpoints**

#### **5.1 Dashboard Overview**
**GET** `/api/dashboard`
- **Description**: Retrieves an overview of job search progress.
- **Response**:
```json
{
  "totalApplications": 12,
  "statuses": {
    "Applied": 8,
    "Interviewed": 3,
    "Offered": 1
  }
}
```
- **Authentication**: Required.

---

## **6. Search and Filtering**

### **Endpoints**

#### **6.1 Search Applications**
**GET** `/api/applications/search`
- **Description**: Searches job applications by keyword.
- **Query Parameters**: `?q=InnovateTech`
- **Response**:
```json
[
  {
    "id": 1,
    "companyName": "InnovateTech",
    "jobTitle": "Full Stack Developer"
  }
]
```
- **Authentication**: Required.

---

## **7. Notes**

### **Endpoints**

#### **7.1 Add Notes**
**POST** `/api/applications/:id/notes`
- **Description**: Adds a note to a job application.
- **Request Body**:
```json
{
  "note": "Discussed the company culture and team structure."
}
```
- **Response**:
```json
{
  "message": "Note added successfully",
  "note": {
    "id": 1,
    "applicationId": 1,
    "note": "Discussed the company culture and team structure."
  }
}
```
- **Authentication**: Required.
