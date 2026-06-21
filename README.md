# My Portfolio & Admin Panel

A fully functional, responsive portfolio website with an integrated admin dashboard, built with **HTML**, **Tailwind CSS**, **JavaScript**, and **Firebase** (Realtime Database, Authentication, and Storage).

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
  - [Public Portfolio](#public-portfolio)
  - [Admin Panel](#admin-panel)
  - [Access Control & Roles](#access-control--roles)
- [Technology Stack](#technology-stack)
- [Firebase Configuration](#firebase-configuration)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Firebase Setup](#firebase-setup)
- [Usage](#usage)
  - [Public View](#public-view)
  - [Admin Login](#admin-login)
  - [Managing Projects](#managing-projects)
  - [Inbox / Messages](#inbox--messages)
  - [Settings](#settings)
  - [Access Control](#access-control)
- [Role-Based Permissions](#role-based-permissions)
- [Mobile Responsiveness](#mobile-responsiveness)
- [Project Structure](#project-structure)
- [Customization](#customization)
- [Troubleshooting](#troubleshooting)
- [License](#license)

---

## Overview

This project is a single-page portfolio website that includes:
- A **public-facing portfolio** showcasing your profile, skills, projects, and contact form.
- A **secure admin panel** protected by Firebase Authentication.
- **Role-based access control** with three user roles: Admin, Editor, and Viewer.
- Real-time data synchronization using **Firebase Realtime Database**.
- Image upload support via **Firebase Storage** or Base64 encoding.
- Browser notification support for new contact form submissions.

---

## Features

### Public Portfolio

| Section | Description |
|---------|-------------|
| **Home** | Hero section with your name, title, profile image, and social links. |
| **About** | Detailed bio, skills with progress bars, and an about image. |
| **Projects** | Grid layout displaying your projects with images, categories, and links. |
| **Contact** | Functional contact form that stores messages in Firebase. |
| **Footer** | Quick links and social media connections. |

### Admin Panel

| Section | Description |
|---------|-------------|
| **Dashboard** | Overview stats: total projects, new messages, site visits, and pending tasks. |
| **Projects** | Add, edit, delete projects with image upload (drag & drop supported). |
| **Inbox** | View, star, mark read/unread, reply via email, and delete messages. Bulk actions supported. |
| **Settings** | Update profile info, social links, skills, profile picture, and about page image. |
| **Access Control** | Manage admin users, assign roles, and view permission matrix. |

### Access Control & Roles

The system supports three distinct user roles:

- **Admin** — Full access to all features including user management.
- **Editor** — Can manage projects and messages but cannot access settings or user management.
- **Viewer** — Read-only access to dashboard, projects, and messages.

---

## Technology Stack

| Technology | Purpose |
|------------|---------|
| **HTML5** | Page structure and semantic markup |
| **Tailwind CSS** | Utility-first CSS framework for styling |
| **Font Awesome 6** | Icons throughout the interface |
| **Google Fonts (Inter)** | Typography |
| **Firebase App (v9 compat)** | Core Firebase SDK |
| **Firebase Realtime Database** | Real-time data storage |
| **Firebase Authentication** | Email/password user authentication |
| **Firebase Storage** | Image file storage (optional) |
| **Vanilla JavaScript** | All application logic |

---

## Firebase Configuration

The project uses the following Firebase configuration (already embedded in the HTML):

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyBs6BQeJrS6wkMifhQ2cRF8tmZecVBbSE8",
    authDomain: "abdullahi-umar-profolio.firebaseapp.com",
    databaseURL: "https://abdullahi-umar-profolio-default-rtdb.firebaseio.com",
    projectId: "abdullahi-umar-profolio",
    storageBucket: "abdullahi-umar-profolio.firebasestorage.app",
    messagingSenderId: "1081189087507",
    appId: "1:1081189087507:web:fab3da5c9c7ae87144c2e6",
    measurementId: "G-P6MH203VFE"
};
```

> **Note:** Replace this with your own Firebase project configuration for production use.

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Safari, Edge)
- A Firebase account (free tier is sufficient)
- Basic knowledge of HTML/JavaScript (for customization)

### Installation

1. **Download or clone** this repository.
2. Open the `index.html` file in your browser, **or** deploy to any static hosting service (GitHub Pages, Netlify, Vercel, Firebase Hosting, etc.).
3. No build step is required — the project runs entirely in the browser.

### Firebase Setup

1. Go to [Firebase Console](https://console.firebase.google.com/) and create a new project.
2. Enable **Email/Password Authentication** in the Authentication section.
3. Create a **Realtime Database** and set the security rules (see below).
4. (Optional) Enable **Firebase Storage** for image hosting.
5. Replace the `firebaseConfig` object in the HTML with your project's credentials.

#### Recommended Database Rules

```json
{
  "rules": {
    "portfolio": {
      ".read": true,
      ".write": "auth != null",
      "adminUsers": {
        ".read": "auth != null",
        ".write": "auth != null"
      }
    }
  }
}
```

> **Warning:** The rules above allow public read access to portfolio data. Adjust according to your privacy needs.

---

## Usage

### Public View

When visitors open the site, they see:
- Your hero section with name and title
- About section with bio and skills
- Projects gallery
- Contact form (messages are saved to Firebase in real-time)

### Admin Login

1. Click the **"Admin"** button in the top navigation.
2. Enter your email and password.
3. Upon successful login, the admin dashboard appears.

> The first user to log in is automatically assigned the **Admin** role.

### Managing Projects

1. Navigate to **Projects** in the admin sidebar.
2. Click **"Add Project"** to open the modal.
3. Fill in the project details:
   - Upload an image (drag & drop supported) or paste an image URL
   - Title, category, description, and optional project link
4. Click **"Save Project"**.
5. To edit or delete, use the action buttons in the project list.

### Inbox / Messages

1. Navigate to **Inbox** in the admin sidebar.
2. New messages appear in real-time.
3. Actions available:
   - **Star** important messages
   - **Mark as read/unread**
   - **Reply** (opens your default email client)
   - **Delete** individual or bulk messages
   - **Filter** by All, Unread, or Starred

### Settings

1. Navigate to **Settings** in the admin sidebar.
2. Update your:
   - Profile picture (upload or drag & drop)
   - Name, title, email, phone, location
   - Bio text
   - Social media links (GitHub, LinkedIn, Twitter, Instagram)
   - Skills with proficiency percentages
   - About page image
3. Click **"Save Changes"** to update the public portfolio instantly.

### Access Control

1. Navigate to **Access Control** (Admin only).
2. View current admin users and their roles.
3. Click **"Add User"** to create new admin accounts.
4. Use the **Edit** button to change a user's role.
5. Use the **Delete** button to remove a user.

---

## Role-Based Permissions

| Permission | Admin | Editor | Viewer |
|------------|:-----:|:------:|:------:|
| View Dashboard | ✅ | ✅ | ✅ |
| Manage Projects (Add/Edit/Delete) | ✅ | ✅ | ❌ |
| View Messages | ✅ | ✅ | ✅ |
| Reply to Messages | ✅ | ✅ | ❌ |
| Delete Messages | ✅ | ✅ | ❌ |
| Edit Profile Settings | ✅ | ❌ | ❌ |
| Manage Access Control | ✅ | ❌ | ❌ |
| Add/Remove Users | ✅ | ❌ | ❌ |
| Change User Roles | ✅ | ❌ | ❌ |

---

## Mobile Responsiveness

The application is fully responsive and optimized for mobile devices:

- **Touch-friendly** buttons (minimum 44px tap targets)
- **Swipe gestures** for admin sidebar (swipe left to close, swipe right from edge to open)
- **Bottom navigation bar** for admin panel on mobile
- **Responsive tables** that convert to card layouts on small screens
- **Optimized form inputs** (16px font size to prevent iOS zoom)
- **Safe area insets** support for notched devices

---

## Project Structure

```
my-portfolio/
│
├── index.html          # Main application file (contains all HTML, CSS, and JS)
├── README.md           # This file
│
└── (No build tools required - all dependencies loaded via CDN)
```

> **Note:** This is a single-file application. All HTML, CSS, and JavaScript are contained within `index.html` for simplicity and ease of deployment.

---

## Customization

### Changing Colors

The primary color is defined in the Tailwind config (inside the `<script>` tag):

```javascript
tailwind.config = {
    theme: {
        extend: {
            colors: { primary: '#3b82f6' }  // Change this hex code
        }
    }
}
```

### Changing the Brand Name

Search for `"MyPortfolio"` in the HTML and replace with your desired brand name.

### Adding More Social Links

In the Settings page, add new input fields and update the `social` object in `saveSettings()`.

### Changing Default Data

Modify the `useDefaultData()` function to set your default profile information.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| **Firebase PERMISSION_DENIED** | Check your database rules. Ensure `.read` is set to `true` or `auth != null` as needed. |
| **Images not uploading** | Check Firebase Storage rules. For Base64 images, ensure they are under 1MB for best performance. |
| **Admin panel not loading** | Verify Firebase config credentials. Check browser console for errors. |
| **Contact form not working** | Ensure Firebase Database is enabled and rules allow writes. |
| **Notifications not showing** | Browser notifications require HTTPS (except on localhost). Check Notification permissions in browser settings. |
| **Loading screen stuck** | Check internet connection. Firebase CDN scripts must load successfully. |

---

## License

This project is open source and available under the [MIT License](LICENSE).

---

## Credits

- Built with [Tailwind CSS](https://tailwindcss.com)
- Icons by [Font Awesome](https://fontawesome.com)
- Backend by [Firebase](https://firebase.google.com)
- Font by [Google Fonts - Inter](https://fonts.google.com/specimen/Inter)

---

**Author:** Abdullahi Umar  
**Project:** My Portfolio & Admin Panel  
**Year:** 2026
