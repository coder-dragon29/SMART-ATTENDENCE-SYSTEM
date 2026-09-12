# Smart Attendance System
<img width="1887" height="970" alt="image" src="https://github.com/user-attachments/assets/15b12ea5-aee9-4a58-b041-eae937acb6a6" />

A full-stack **Smart Attendance Management System** designed to simplify classroom attendance using secure authentication, real-time attendance sessions, dashboards, reports, and browser-based face recognition.

The project includes a modern frontend and a Node.js/Express REST API backend, making it suitable for college projects, hackathons, academic demonstrations, and future production expansion.

---

## Features

### Student Features

* Student registration and login
* Student dashboard
* View attendance statistics
* View attendance history
* Track attendance percentage
* Join active attendance sessions
* Face ID enrollment using webcam
* Automatic attendance marking through face recognition

### Teacher Features

* Teacher registration and login
* Create and manage attendance sessions
* Start and end classroom sessions
* View live attendance
* Mark attendance manually or using face recognition
* Class-wise attendance reports
* Date-wise attendance reports
* View recent sessions and attendance statistics

### System Features

* JWT-based authentication
* Password hashing using bcrypt
* RESTful API architecture
* Persistent JSON-based data storage
* CORS support
* Login rate limiting
* Browser-based face recognition using `face-api.js`
* No student images or videos are uploaded to the backend
* Responsive web interface

---

## Technology Stack

### Frontend

* HTML5
* CSS3
* JavaScript
* Face API.js
* Browser Webcam API

### Backend

* Node.js
* Express.js
* JWT
* bcryptjs
* dotenv
* CORS
* Express Rate Limit

### Database

* Local JSON file storage
* Easily replaceable with MongoDB, PostgreSQL, or another database

---

## Project Structure

```text
smart-attendance-project/
│
├── frontend/
│   ├── index.html
│   ├── index.js
│   ├── index.css
│   ├── common.js
│   ├── config.js
│   ├── face.js
│   │
│   ├── student-login.html
│   ├── student-login.js
│   ├── student-dashboard.html
│   ├── student-dashboard.js
│   ├── student-dashboard.css
│   │
│   ├── teacher-login.html
│   ├── teacher-login.js
│   ├── teacher-dashboard.html
│   ├── teacher-dashboard.js
│   ├── teacher-dashboard.css
│   │
│   └── assets/
│
├── backend/
│   ├── package.json
│   ├── .env.example
│   ├── README.md
│   │
│   └── src/
│       ├── app.js
│       ├── server.js
│       ├── config/
│       ├── controllers/
│       ├── db/
│       ├── middleware/
│       ├── routes/
│       └── utils/
│
└── README.md
```

---

## How Face Recognition Works

The system uses browser-based face recognition to identify enrolled students.

### Face Enrollment

1. The student opens the Face ID Enrollment section.
2. The webcam captures the student's face.
3. `face-api.js` generates a 128-dimensional face descriptor.
4. Only the numerical descriptor is sent to the backend.
5. No image or video is stored on the server.

### Attendance Recognition

1. A teacher starts an attendance session.
2. The teacher activates the camera.
3. The browser loads enrolled student face descriptors.
4. The current camera frame is compared against known descriptors.
5. If a match is found, attendance is marked automatically.

> Face matching is performed locally in the browser. The backend stores only face descriptor data, not photographs or videos.

---

## Requirements

Make sure the following are installed:

* Node.js version 18 or higher
* npm
* A modern web browser
* Webcam for Face ID functionality

---

## Installation and Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/smart-attendance-project.git
cd smart-attendance-project
```

### 2. Setup Backend

```bash
cd backend
npm install
```

Create the environment file:

```bash
cp .env.example .env
```

For Windows, manually copy `.env.example` to `.env` if required.

Update the `.env` file according to your configuration.

### 3. Seed Demo Accounts (Optional)

```bash
npm run seed
```

This creates sample login accounts for testing.

### 4. Start the Backend

For development:

```bash
npm run dev
```

For production-style execution:

```bash
npm start
```

The backend will run at:

```text
http://localhost:5000
```

### 5. Start the Frontend

Open a new terminal:

```bash
cd frontend
```

You can use any static server.

Using `npx serve`:

```bash
npx serve .
```

Or using Python:

```bash
python -m http.server 3000
```

You can also use the **Live Server** extension in Visual Studio Code.

---

## Configuration

Open:

```text
frontend/config.js
```

Update the backend URL if necessary:

```javascript
const API_BASE = "http://localhost:5000";
```

The frontend must point to the correct backend address.

Also ensure that the frontend origin is included in the backend's `CORS_ORIGIN` configuration.

Example:

```env
CORS_ORIGIN=http://localhost:3000
```

---

## Demo Credentials

After running:

```bash
npm run seed
```

You can use:

### Teacher

```text
Email: demo.teacher@college.edu
Password: password123
```

### Student

```text
Roll Number: CSE5001
Password: password123
```

---

## API Overview

### Authentication

| Method | Endpoint                     | Description        |
| ------ | ---------------------------- | ------------------ |
| POST   | `/api/auth/student/register` | Register a student |
| POST   | `/api/auth/student/login`    | Student login      |
| POST   | `/api/auth/teacher/register` | Register a teacher |
| POST   | `/api/auth/teacher/login`    | Teacher login      |
| GET    | `/api/auth/me`               | Get current user   |

### Sessions

| Method | Endpoint                       | Description               |
| ------ | ------------------------------ | ------------------------- |
| POST   | `/api/sessions`                | Create attendance session |
| GET    | `/api/sessions`                | Get sessions              |
| GET    | `/api/sessions/active`         | Get active session        |
| GET    | `/api/sessions/:sessionId`     | Get session details       |
| PATCH  | `/api/sessions/:sessionId/end` | End a session             |

### Attendance

| Method | Endpoint                              | Description                        |
| ------ | ------------------------------------- | ---------------------------------- |
| POST   | `/api/attendance/mark`                | Mark attendance as student         |
| POST   | `/api/attendance/mark-manual`         | Mark attendance manually/by camera |
| GET    | `/api/attendance/session/:sessionId`  | View session attendance            |
| GET    | `/api/attendance/student/:rollNumber` | View student attendance history    |
| GET    | `/api/attendance/reports/class`       | Class attendance report            |
| GET    | `/api/attendance/reports/date`        | Date-wise attendance report        |

### Dashboards

| Method | Endpoint                 | Description            |
| ------ | ------------------------ | ---------------------- |
| GET    | `/api/dashboard/student` | Student dashboard data |
| GET    | `/api/dashboard/teacher` | Teacher dashboard data |

---

## Security

The project includes:

* JWT authentication
* Password hashing using bcrypt
* Protected API routes
* Role-based authorization
* Login rate limiting
* CORS configuration
* No plaintext password storage

---

## Current Limitations

This project is currently optimized for academic and hackathon demonstrations.

* Data is stored in a local JSON file.
* Face recognition works with one face at a time.
* Face recognition accuracy depends on lighting and camera angle.
* Face models are loaded from a public CDN by default.
* A production deployment should use a proper database and stronger infrastructure.

---

## Future Improvements

* MongoDB/PostgreSQL integration
* Multi-face recognition in a single frame
* Cloud deployment
* Admin dashboard
* Attendance export to Excel/PDF
* Email notifications
* QR code attendance
* Mobile application
* Advanced analytics and charts
* Improved anti-spoofing/liveness detection
* Offline face model support

---

## Use Cases

* College classroom attendance
* School attendance management
* University departments
* Coaching institutes
* Training centers
* Hackathon demonstrations
* Smart campus applications

---

## Screenshots

Add screenshots of your project here:

```markdown
![Home Page](screenshots/home.png)
![Student Dashboard](screenshots/student-dashboard.png)
![Teacher Dashboard](screenshots/teacher-dashboard.png)
![Face Recognition](screenshots/face-recognition.png)
```

---

## Contributing

Contributions are welcome.

1. Fork the repository
2. Create a new branch

```bash
git checkout -b feature/new-feature
```

3. Commit your changes

```bash
git commit -m "Add new feature"
```

4. Push to your branch

```bash
git push origin feature/new-feature
```

5. Open a Pull Request

---

## License

This project is available for educational and demonstration purposes.

---

## Author

Team TEJAS 💕
