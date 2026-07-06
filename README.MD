# 🚗 Car Rental System

A full-stack Car Rental System built using the MERN stack that allows users to browse available cars, make bookings, and manage reservations. The application also includes an admin panel for managing cars and monitoring bookings.

---

## 📌 Overview

The Car Rental System is designed to simplify the vehicle rental process by providing an intuitive interface for customers and an efficient management system for administrators.

Users can:
- Register and log in securely.
- Browse available cars.
- View detailed car information.
- Book cars for specific dates.
- View their booking history.

Administrators can:
- Add new cars.
- Update car details.
- Delete or disable cars.
- Manage bookings.
- Monitor the availability of vehicles.

---

## ✨ Features

### User Features

- User Registration & Login
- Secure Authentication
- Browse Available Cars
- View Car Details
- Book Cars
- Booking History
- Responsive User Interface

### Admin Features

- Admin Authentication
- Add New Cars
- Edit Car Details
- Delete Cars
- Manage Bookings
- Update Vehicle Availability

---

## 🛠 Tech Stack

### Frontend

- React.js
- React Router
- Axios
- CSS

### Backend

- Node.js
- Express.js

### Database

- MongoDB
- Mongoose

### Authentication

- JWT (JSON Web Token)
- bcrypt

### Media Storage

- Cloudinary

---

## 📂 Project Structure

```
CarRental-FullStack
│
├── client/
│   ├── public/
│   ├── src/
│   ├── components/
│   ├── pages/
│   └── ...
│
├── server/
│   ├── config/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── utils/
│   └── ...
│
├── README.md
└── package-lock.json
```

---

## ⚙️ Installation

### Clone the Repository

```bash
git clone https://github.com/yourusername/car-rental-system.git
```

### Navigate to the Project

```bash
cd car-rental-system
```

### Install Backend Dependencies

```bash
cd server
npm install
```

### Install Frontend Dependencies

```bash
cd ../client
npm install
```

---

## ▶️ Run the Project

### Start Backend

```bash
cd server
npm run server
```

### Start Frontend

```bash
cd client
npm run dev
```

---


## 🔐 Environment Variables

Create a `.env` file inside the `server` directory and configure the following environment variables:

```env
PORT=5000

MONGODB_URI=<your_mongodb_connection_string>

JWT_SECRET=<your_jwt_secret>

CLOUDINARY_CLOUD_NAME=<your_cloud_name>
CLOUDINARY_API_KEY=<your_cloudinary_api_key>
CLOUDINARY_API_SECRET=<your_cloudinary_api_secret>
```

> **Note:** Never commit your `.env` file or expose sensitive credentials. Ensure `.env` is included in your `.gitignore`.

---

## 📚 API Modules

- Authentication
- User Management
- Car Management
- Booking Management
- Image Upload

---

## 💡 Design Decisions

- Used **JWT Authentication** for stateless and secure user authentication.
- Passwords are encrypted using **bcrypt** before storing them in the database.
- Followed the **MVC architecture** to separate business logic, routes, and database models.
- Used middleware to centralize authentication and authorization logic.
- MongoDB was chosen because of its flexible document structure and seamless integration with Node.js using Mongoose.
- Cloudinary is used for efficient image storage and delivery instead of storing images on the server.

---

## 🚀 Future Improvements

- Online payment integration
- Email notifications
- Car reviews and ratings
- Wishlist/Favorites
- Booking cancellation with refund policy
- Advanced search and filtering
- Real-time availability updates
- Admin analytics dashboard

---


---

## 👨‍💻 Author

**Umang Gupta**

B.Tech ( Data Science)

---

