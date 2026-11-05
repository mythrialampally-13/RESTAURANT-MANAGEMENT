# 🍷 GourmetReserve – Restaurant Reservation System

A full-stack web application designed for restaurant table discovery, real-time booking management, and multi-tier role-based operations (Customer, Restaurant Owner, and Administrator). Built with React.js, Node.js, Express.js, MongoDB, and Bootstrap.

---

## 📌 Table of Contents
1. [Project Overview](#project-overview)
2. [Technologies Used](#technologies-used)
3. [Key Features by Role](#key-features-by-role)
4. [Project Folder Structure](#project-folder-structure)
5. [Prerequisites](#prerequisites)
6. [MongoDB Compass Setup](#mongodb-compass-setup)
7. [Environment Variables](#environment-variables)
8. [Installation & Startup Guide](#installation--startup-guide)
9. [REST API Documentation](#rest-api-documentation)
10. [Automated Testing & Verification](#automated-testing--verification)
11. [College Project Demonstration Workflow](#college-project-demonstration-workflow)

---

## 📖 Project Overview
GourmetReserve bridges the gap between discerning food connoisseurs and fine-dining establishments. Diners can explore curated venues, filter by cuisine and city, select custom dining areas (e.g., Rooftop Terrace, Wine Cellar, Main Hall), and submit reservations with special requests. 

The application enforces a real-world multi-stage booking lifecycle:
$$\text{Customer Submits Booking} \longrightarrow \text{Status: Pending} \longrightarrow \text{Owner Approves/Rejects} \longrightarrow \text{Status: Confirmed/Rejected}$$

---

## 🚀 Technologies Used

### Frontend
- **React.js 18** (Functional components, Hooks, Context API)
- **Bootstrap 5 & Bootstrap Icons** (Responsive grid, elegant badges, cards, navigation)
- **HTML5 & Modern CSS3** (Custom editorial restaurant palette: warm ivory `#fbf9f5`, deep burgundy `#6c1420`, gold highlights `#c59b27`)
- **Native Fetch API** (Centralized async communication with error interceptors)
- **Vite** (Next-generation lightning-fast frontend tooling)

### Backend
- **Node.js & Express.js** (RESTful API architecture)
- **Node.js Native Crypto Module** (`scrypt` password hashing + HMAC-SHA256 signed JWT tokens)
- **CORS & Dotenv** (Cross-origin resource sharing & configuration management)
- **Validator** (Strict input and email sanitization)

### Database
- **MongoDB** (NoSQL document database on port `27017`)
- **Mongoose ODM** (Schema modeling, relational references, query validation)
- **MongoDB Compass** (GUI database inspection)

---

## 👥 Key Features by Role

### 1. 🍽️ Customer Module
- **Registration & Authentication**: Name, email, phone, secure password hashing, duplicate email prevention.
- **Venue Discovery**: Browse restaurants with live keyword search, cuisine filtering, and city selection.
- **Restaurant Details**: View image galleries, operating hours, contact details, and available dining areas.
- **Table Booking**: Select reservation date (past dates blocked), seating times, party size (1–50), and dining sections.
- **Initial Status Control**: All new reservations start in **Pending** status.
- **My Reservations**: View booking history with status badges (`Pending`, `Confirmed`, `Rejected`, `Cancelled`).
- **Cancellation**: Diners can cancel their own eligible bookings.
- **Profile Management**: Update full name and contact phone number.

### 2. 👨‍🍳 Restaurant Owner Module
- **Owner Dashboard**: Live metrics for Total, Pending, Confirmed, Rejected, and Cancelled requests.
- **Manage Restaurant**: Update description, cuisine, street address, operating hours, dining sections, and image URLs.
- **Reservation Approvals**: Review customer requests with one-click **Approve** or **Reject** actions.
- **Ownership Security**: Owners can only view and manage reservations belonging to their own assigned restaurant.

### 3. 🛡️ Administrator Module
- **Executive Analytics**: System counters for total registered customers, owners, venues, and reservations.
- **User Account Management**: Search users, filter by role (`customer`, `owner`, `admin`), change permissions, or remove accounts.
- **Restaurant Catalog Vetting**: Approve or reject restaurant listings before they go live on the public site.
- **Master Reservation Ledger**: Audit platform-wide bookings and resolve diner inquiries.

---

## 📂 Project Folder Structure

```text
RESTRAUNT MANAGEMENT/
├── package.json                   # Root package configuration
├── README.md                      # Complete project documentation
│
├── backend/
│   ├── package.json               # Backend dependencies
│   ├── server.js                  # Entry point (port 5000, DB connection)
│   ├── app.js                     # Express app setup & route mounting
│   ├── seed.js                    # Database seeder with demo accounts & restaurants
│   ├── test_suite.js              # Automated 27-point verification audit script
│   │
│   ├── config/
│   │   ├── config.env             # Environment variables
│   │   └── db.js                  # Mongoose MongoDB connection
│   │
│   ├── models/
│   │   ├── userModel.js           # User schema (customer, owner, admin)
│   │   ├── restaurantModel.js     # Restaurant schema with dining areas & availability
│   │   └── reservationModel.js    # Reservation schema with status workflow
│   │
│   ├── controllers/
│   │   ├── userController.js      # Auth, profile, and registration logic
│   │   ├── restaurantController.js# Restaurant CRUD and approval logic
│   │   ├── reservationController.js# Reservation booking, status updates & cancellations
│   │   └── adminController.js     # Metrics and user management logic
│   │
│   ├── routes/
│   │   ├── userRoutes.js          # /api/v1/user
│   │   ├── restaurantRoutes.js    # /api/v1/restaurant
│   │   ├── reservationRoutes.js   # /api/v1/reservation
│   │   └── adminRoutes.js         # /api/v1/admin
│   │
│   ├── middleware/
│   │   ├── authMiddleware.js      # JWT authentication & role-based authorization
│   │   └── errorMiddleware.js     # 404 handler & Mongoose CastError / duplicate key handler
│   │
│   └── utils/
│       └── authHelper.js          # scrypt password hashing & HMAC JWT tokens
│
└── frontend/
    ├── package.json               # Frontend dependencies (React, Bootstrap, Vite)
    ├── vite.config.js             # Vite configuration
    ├── index.html                 # HTML5 template with Google typography
    │
    └── src/
        ├── main.jsx               # React 18 DOM root & provider mounting
        ├── App.jsx                # Global routing & layout wrapper
        ├── api.js                 # Centralized fetch API client
        ├── index.css              # Custom editorial restaurant theme & styling
        │
        ├── context/
        │   ├── AuthContext.jsx    # Persistent auth state (login/logout/update)
        │   └── NavigationContext.jsx # Reactive browser navigation context
        │
        ├── components/
        │   ├── Navbar.jsx         # Responsive navigation bar with role-specific items
        │   ├── Footer.jsx         # Luxury footer with branding & links
        │   ├── RestaurantCard.jsx # Dynamic card with cuisine badges & actions
        │   ├── BookingForm.jsx    # Form with date, guest, and section validation
        │   └── ProtectedRoute.jsx # Role-based page access guard
        │
        └── pages/
            ├── Home.jsx           # Hero, featured venues, How-It-Works, testimonials
            ├── About.jsx          # Heritage, platform pillars, and vision
            ├── Contact.jsx        # Concierge contact & inquiry form
            ├── Login.jsx          # Multi-role sign in + 1-click demo test buttons
            ├── Register.jsx       # Customer & Owner registration form
            ├── Restaurants.jsx    # Live catalog with keyword, cuisine, and city filters
            ├── RestaurantDetails.jsx # Image gallery, dining sections & embedded booking
            │
            ├── customer/
            │   ├── CustomerDashboard.jsx  # Counters & recent bookings
            │   ├── CustomerProfile.jsx    # Edit personal info
            │   └── MyReservations.jsx     # Status badges & booking cancellation
            │
            ├── owner/
            │   ├── OwnerDashboard.jsx     # Reservation metrics & quick approval
            │   ├── ManageRestaurant.jsx   # Add/edit restaurant profile & sections
            │   └── ManageReservations.jsx # Tabbed approval/rejection ledger
            │
            └── admin/
                ├── AdminDashboard.jsx     # System-wide metrics
                ├── ManageUsers.jsx        # User account control & role editing
                ├── ManageRestaurants.jsx  # Approve/reject venue listings
                └── ManageReservations.jsx # Master platform reservation ledger
```

---

## 🗄️ MongoDB Compass Setup
1. Launch **MongoDB Compass**.
2. Set connection string to:
   ```text
   mongodb://127.0.0.1:27017
   ```
3. Click **Connect**.
4. You will observe the `restaurant_db` database containing three collections:
   - `users` (Admin, Owner, and Customer documents)
   - `restaurants` (Featured dining establishments with seating areas and hours)
   - `reservations` (Real-time bookings linked by relational ObjectIDs)

---

## ⚙️ Environment Variables
Located in `backend/config/config.env`:
```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://127.0.0.1:27017/restaurant_db
JWT_SECRET=btech_college_restaurant_reservation_jwt_secret_key_2026
FRONTEND_URL=http://localhost:5173
```

---

## 💻 Installation & Startup Guide

### 1. Database Seeding (Populate Initial Records)
Open a terminal in the root folder and run:
```bash
npm run seed
```
*(Seeds 4 featured restaurants, demo user accounts, and sample reservations).*

### 2. Start the Backend API Server
```bash
npm run server
```
*Backend runs on `http://localhost:5000`.*

### 3. Start the Frontend Application
In a separate terminal window:
```bash
npm run client
```
*Frontend runs on `http://localhost:5173`.*

---

## 📡 REST API Documentation

### Authentication (`/api/v1/user`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/user/register` | Public | Register customer or restaurant owner |
| `POST` | `/api/v1/user/login` | Public | Sign in & receive signed JWT |
| `GET` | `/api/v1/user/profile` | Private | Retrieve logged-in profile |
| `PUT` | `/api/v1/user/profile` | Private | Update name or phone number |

### Restaurants (`/api/v1/restaurant`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/v1/restaurant` | Public | List approved venues with search & filter |
| `GET` | `/api/v1/restaurant/:id` | Public | Get venue details by ID |
| `GET` | `/api/v1/restaurant/owner/my` | Owner | Get restaurant owned by logged-in user |
| `POST` | `/api/v1/restaurant` | Owner/Admin | Create new restaurant listing |
| `PUT` | `/api/v1/restaurant/:id` | Owner/Admin | Update existing restaurant details |
| `DELETE`| `/api/v1/restaurant/:id` | Owner/Admin | Remove restaurant listing |
| `PUT` | `/api/v1/restaurant/:id/approval`| Admin | Update approval (`Approved`, `Rejected`) |

### Reservations (`/api/v1/reservation`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/v1/reservation` | Customer | Submit new booking (Initial status: `Pending`) |
| `GET` | `/api/v1/reservation/my` | Customer | View customer's own reservations |
| `GET` | `/api/v1/reservation/owner` | Owner | View bookings for owner's restaurant |
| `GET` | `/api/v1/reservation/all` | Admin | View platform-wide reservations |
| `GET` | `/api/v1/reservation/:id` | Private | View reservation by ID (Authorized roles) |
| `PUT` | `/api/v1/reservation/:id/status` | Owner/Admin | Approve (`Confirmed`) or decline (`Rejected`) |
| `PUT` | `/api/v1/reservation/:id/cancel` | Customer | Cancel customer reservation |

### Admin (`/api/v1/admin`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/v1/admin/stats` | Admin | Dashboard platform analytics counters |
| `GET` | `/api/v1/admin/users` | Admin | View & search all registered accounts |
| `PUT` | `/api/v1/admin/users/:id` | Admin | Modify user role or details |
| `DELETE`| `/api/v1/admin/users/:id` | Admin | Delete user account |

---

## 🧪 Automated Testing & Verification
The project includes an automated 27-point verification suite checking every functional, security, and schema constraint.
To run the automated audit:
```bash
cd backend
node test_suite.js
```
**Verification Checklist Coverage:**
- [x] 1. Backend starts successfully
- [x] 2. MongoDB connection established
- [x] 3. Frontend builds with 0 errors (`npm run build`)
- [x] 4. Customer registration works
- [x] 5. Duplicate registration rejected
- [x] 6. Login works for each role (Customer, Owner, Admin)
- [x] 7. Invalid login displays 401 error
- [x] 8. Protected pages and APIs reject unauthorized access (401/403)
- [x] 9. Customers can browse dynamic restaurants
- [x] 10. Restaurant details display correctly
- [x] 11. Table booking form functions properly
- [x] 12. Reservations saved to MongoDB
- [x] 13. New reservations strictly start in `Pending` status
- [x] 14. Customers can view their reservations
- [x] 15. Customers can cancel eligible bookings
- [x] 16. Owners can view reservations for their venue
- [x] 17. Owners can approve reservations (`Confirmed`)
- [x] 18. Owners can reject reservations (`Rejected`)
- [x] 19. Cross-owner security check verified (Owner cannot touch other venues)
- [x] 20. Admin dashboard displays accurate platform metrics
- [x] 21. Admin can approve and reject restaurant listings
- [x] 22. Role-based middleware prevents route privilege escalation
- [x] 23. Real-time search and multi-parameter filtering work
- [x] 24. Form validation for emails, passwords, dates, and party size
- [x] 25. All action buttons perform intended backend state transitions
- [x] 26. Responsive Bootstrap layout across mobile and desktop
- [x] 27. Complete reservation schema and relational references preserved

---

## 🎯 College Project Demonstration Workflow

For your demonstration to the evaluators, follow this recommended walkthrough:

### Step 1: Public Discovery
1. Open `http://localhost:5173`.
2. Showcase the **Home Page**: Hero search, dynamically rendered featured restaurants from MongoDB, How It Works, Why Choose Us, and Testimonials.
3. Click **Restaurants** in the navbar to demonstrate live searching by keyword, cuisine dropdown (Italian, French, Indian, Japanese), and city filters.
4. Click **Details** on any venue (e.g. *L’Osteria Bella Vita*) to inspect photo gallery, seating areas (*Chef's Counter, Private Wine Cellar*), and operating hours.

### Step 2: Customer Booking & Status Tracking
1. Click **Sign In** and use the **1-Click Customer Demo Fill** button (`customer@gmail.com`).
2. Navigate to *L’Osteria Bella Vita*, select a future date, time (*07:30 PM*), party size (*4 Guests*), and section (*Private Wine Cellar*).
3. Submit the reservation.
4. Point out that the booking confirmation explicitly indicates status: **Pending**.
5. Navigate to **Customer Dashboard** / **My Reservations** to view the pending badge.

### Step 3: Owner Review & Approval
1. Click **Sign Out**, then **Sign In**.
2. Click the **1-Click Owner Demo Fill** button (`owner@bistrogold.com`).
3. Point out the **Owner Dashboard** counters (Total, Pending, Confirmed).
4. Navigate to **Bookings** to show the incoming customer request.
5. Click **Approve**. The status dynamically transitions to **Confirmed**.
6. Demonstrate editing restaurant details under **Manage Restaurant**.

### Step 4: Diner Synchronized Update
1. Sign back into the **Customer** account (`customer@gmail.com`).
2. Open **My Reservations**: show that the badge has updated in real-time to **Confirmed** (green).
3. Demonstrate customer cancellation on an eligible booking to show status changing to **Cancelled**.

### Step 5: Administrator Oversight & MongoDB Compass
1. Sign in as **Admin** (`admin@restaurant.com`).
2. Show the **Admin Dashboard** with real-time aggregate statistics across all collections.
3. Open **Manage Users** to demonstrate role filtering and account controls.
4. Open **Restaurants** to demonstrate approving or rejecting venue submissions.
5. Open **MongoDB Compass** alongside the browser to show the evaluator the raw documents in `users`, `restaurants`, and `reservations` updating in real-time!
`

Follow these steps exactly. Open 3 separate terminals in VS Code. Keep all three running.
Terminal 1 — MongoDB
Copy and execute:
New-Item -ItemType Directory -Force "C:\Users\Sruthi Alampally\data\db"


Then execute:
& "C:\Program Files\MongoDB\Server\9.0\bin\mongod.exe" --dbpath "C:\Users\Sruthi Alampally\data\db" --bind_ip 127.0.0.1 --port 27017


Wait until you see:
Waiting for connections


Terminal 2 — Backend
Open a second terminal and copy:
cd "C:\Users\Sruthi Alampally\OneDrive\Desktop\RESTRAUNT MANAGEMENT\backend"


Then:
npm install


Then:
node server.js


Expected output:
Server started on port 5000
MongoDB Connected successfully


Terminal 3 — Frontend
Open a third terminal and copy:
cd "C:\Users\Sruthi Alampally\OneDrive\Desktop\RESTRAUNT MANAGEMENT\frontend"


Then:
npm install


Then:
npm run dev


Expected output:
Local: http://localhost:5173/


Open this in Chrome:
http://localhost:5173/#   R E S T A U R A N T - M A N A G E M E N T  
 