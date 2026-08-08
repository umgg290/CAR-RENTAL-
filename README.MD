# 🚗 Car Rental System
 
A full-stack Car Rental System built using the MERN stack that allows users to browse available cars, make bookings, and manage reservations. The application also includes an owner panel for listing cars and managing bookings.
 
**Live Demo:** _add your deployed link here_
**Repo:** _add your GitHub repo URL here_
 
---
 
## 📌 Overview
 
The Car Rental System simplifies the vehicle rental process with an intuitive interface for renters and an efficient management flow for car owners. Any registered user can become an owner and start listing cars — there's no separate admin signup.
 
Users can:
- Register and log in securely
- Browse available cars, filtered by location and date range
- View detailed car information
- Book cars for specific dates
- View their booking history
Owners can:
- Switch their account role to "owner"
- Add new car listings with an image
- Toggle car availability
- View and update the status of incoming bookings
- See a dashboard with total cars, bookings, and monthly revenue
---
 
## ✨ Features
 
### User Features
- User Registration & Login (JWT-based sessions)
- Secure password hashing (bcrypt)
- Browse cars by location and availability window
- View car details
- Book cars for a date range
- View booking history
- Responsive UI (Tailwind CSS)
### Owner Features
- Become an owner from any user account
- Add new cars with image upload
- Toggle car availability on/off
- Soft-delete a car listing
- View and update booking status (pending / confirmed / cancelled)
- Dashboard: total cars, total bookings, pending/confirmed counts, recent bookings, monthly revenue
---
 
## 🛠 Tech Stack
 
### Frontend
- React 19 + Vite
- React Router
- Axios
- Tailwind CSS v4
- Framer Motion (`motion`)
- react-hot-toast
### Backend
- Node.js
- Express 5
### Database
- MongoDB + Mongoose
### Authentication
- JWT (JSON Web Token)
- bcrypt
### Media Storage
- **ImageKit** — image upload with on-the-fly optimization (resize, auto-compress, WebP conversion). Files are received via Multer, uploaded to ImageKit, and only the resulting URL is stored in MongoDB.
### Deployment
- Vercel (both `client/` and `server/` include a `vercel.json`)
---
 
## 📂 Project Structure
 
```
CAR-RENTAL--main
│
├── client/
│   ├── public/
│   └── src/
│       ├── assets/
│       ├── components/
│       ├── components/owner/
│       ├── context/        # AppContext - auth/user state
│       └── pages/
│           └── owner/
│
├── server/
│   ├── configs/            # db.js, imageKit.js
│   ├── controllers/        # userController, ownerController, bookingController
│   ├── middleware/         # auth.js (JWT protect), multer.js
│   ├── models/             # User, Car, Booking
│   ├── routes/             # userRoutes, ownerRoutes, bookingRoutes
│   └── server.js
│
├── README.md
└── package-lock.json
```
 
---
 
## ⚙️ Installation
 
### Clone the Repository
 
```bash
git clone <your-repo-url>
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
 
Create a `.env` file inside the `server` directory:
 
```env
PORT=3000
 
MONGODB_URI=<your_mongodb_connection_string>
 
JWT_SECRET=<your_jwt_secret>
 
IMAGEKIT_PUBLIC_KEY=<your_imagekit_public_key>
IMAGEKIT_PRIVATE_KEY=<your_imagekit_private_key>
IMAGEKIT_URL_ENDPOINT=<your_imagekit_url_endpoint>
```
 
> **Note:** Never commit your `.env` file or expose sensitive credentials. Ensure `.env` is included in your `.gitignore`.
 
---
 
## 📚 API Reference
 
Base URL: `/api`
 
All protected routes require the JWT in the `Authorization` header (raw token, not `Bearer <token>`).
 
### User routes — `/api/user`
 
| Method | Endpoint    | Auth | Description                          |
|--------|-------------|------|--------------------------------------|
| POST   | `/register` | No   | Register a new user                  |
| POST   | `/login`    | No   | Log in, returns JWT                  |
| GET    | `/data`     | Yes  | Get logged-in user's profile         |
| GET    | `/cars`     | No   | List all available cars              |
 
### Owner routes — `/api/owner`
 
| Method | Endpoint        | Auth | Description                              |
|--------|-----------------|------|-------------------------------------------|
| POST   | `/change-role`  | Yes  | Promote current user to `owner`           |
| POST   | `/add-car`      | Yes  | Add a new car (multipart, field: `image`) |
| GET    | `/cars`         | Yes  | List cars owned by the current user       |
| POST   | `/toggle-car`   | Yes  | Toggle a car's availability               |
| POST   | `/delete-car`   | Yes  | Soft-delete a car (unassigns owner)       |
| GET    | `/dashboard`    | Yes  | Owner dashboard stats                     |
| POST   | `/update-image` | Yes  | Update the current user's profile image   |
 
### Booking routes — `/api/bookings`
 
| Method | Endpoint              | Auth | Description                                   |
|--------|------------------------|------|-----------------------------------------------|
| POST   | `/check-availability`  | No   | Check available cars for a location/date range |
| POST   | `/create`               | Yes  | Create a booking                               |
| GET    | `/user`                 | Yes  | List bookings made by the current user         |
| GET    | `/owner`                | Yes  | List bookings for cars the user owns           |
| POST   | `/change-status`        | Yes  | Update a booking's status (owner only)         |
 
---
 
## 💡 Design Decisions
 
- **JWT authentication** for stateless, scalable sessions — verified server-side with `jwt.verify()` on every protected route.
- **bcrypt** hashes passwords before storage; plain text is never persisted.
- **MVC architecture** — routes, controllers, and models are cleanly separated per resource (user, owner, booking).
- **Single User model with a `role` field** instead of separate user/owner collections — any user can become an owner via `/change-role`, avoiding duplicate auth logic.
- **Ownership checks in controllers** — mutating endpoints (toggle/delete car, change booking status) verify the resource's `owner` matches the requester before acting, not just that a valid token was presented.
- **MongoDB + Mongoose** for a flexible schema that fits an evolving car catalog.
- **ImageKit** for image storage and on-the-fly optimization (resize, compress, WebP) instead of storing raw files or multiple pre-generated sizes.
- **Date-range overlap check** for booking availability: a car is unavailable if any existing booking's range overlaps the requested pickup/return window.
---
 
## ⚠️ Known Limitations / Future Improvements
 
- JWTs are not set to expire (`expiresIn` is not configured) — a valid token remains usable indefinitely.
- `deleteCar` is a soft delete (owner is unset, availability set to false); the car document isn't actually removed.
- No request-body validation library (e.g. Zod/Joi) — validation is manual and minimal.
- No automated tests yet.
- Planned: online payment integration, email notifications, car reviews/ratings, wishlist, booking cancellation with refund policy, real-time availability updates.
---
 
## 👨‍💻 Author
 
**Umang Gupta**
B.Tech (Data Science)
