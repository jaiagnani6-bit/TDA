BizSolution Co. - Comprehensive Business Solutions Website

This repository contains a complete, single-file, responsive corporate website built using pure HTML, vanilla JavaScript, and Tailwind CSS. It is designed to function as a fast, client-side Single-Page Application (SPA) with real-time data persistence powered by Google Firebase Firestore.

🚀 Project Overview

The BizSolution Co. website provides essential information about the company's core offerings (Digital Transformation, Cloud, and Security) and offers a functional contact form that logs user inquiries to a live database.

Key Features:

Single-File Architecture: The entire application (HTML, CSS, JS, and configuration) resides in a single index.html file.

Responsive Design: Optimized for mobile, tablet, and desktop viewports using Tailwind CSS.

Client-Side Navigation (SPA): Uses JavaScript for smooth, rapid page transitions without full reloads.

Firebase Integration: Authenticates users and stores contact form submissions securely using Firestore.

Accessible Modals (A11y): Utilizes custom, accessible modal dialogs for service details and form feedback, replacing standard browser alerts.

🛠️ Technology Stack

Component

Technology

Role

Structure/View

HTML5, Tailwind CSS

Layout, Styling, and Responsive Design

Logic

Vanilla JavaScript (ES6+)

Routing, DOM manipulation, Form handling

Database/Auth

Firebase (Firestore & Auth)

Data persistence for inquiries and user authentication

⚙️ Setup and Execution

Since this application is designed for an environment (like Google's Canvas) that provides Firebase credentials automatically, standard local setup requires special attention to the necessary global variables.

Running the Application

Save the File: Save the provided code as index.html.

Open in Browser: Open index.html directly in your web browser.

The application includes checks for the required global variables (__firebase_config, __app_id, __initial_auth_token). If these are not defined, the application will run in a safe "Offline Mode" but the contact form will not submit data.

Firebase Context (Mandatory for Data Persistence)

For the Contact Form to function, the following JavaScript global variables must be defined in the runtime environment:

Global Variable

Purpose

Security

__firebase_config

JSON string of the Firebase project configuration object.

Used for initializing the database connection.

__app_id

Unique ID of the application instance.

Defines the path for data storage (e.g., artifacts/{appId}/...).

__initial_auth_token

Custom Firebase Auth Token.

Used to sign in the user, establishing userId for data operations.

Data is stored in the public collection path:
artifacts/{__app_id}/public/data/inquiries/{documentId}

📝 Key Functions

1. initializeFirebase() (Setup)

This asynchronous function is responsible for:

Parsing the provided Firebase configuration.

Initializing firebase/app, firestore, and auth.

Signing in the user using signInWithCustomToken(__initial_auth_token) or falling back to signInAnonymously().

Setting the userId displayed in the footer and updating the isFirebaseReady state.

2. renderPage(pageKey) (Routing)

Handles the application's client-side routing. It:

Accepts a pageKey (home, services, about, contact).

Injects the corresponding HTML content from the pageContent object into the main area (#app-content).

Uses a setTimeout with a transition for a smooth fade-in/out effect.

Updates the browser URL hash (#pageKey) and the active state of the navigation links.

3. submitContactForm(event) (Data Persistence)

Triggered on form submission, this function:

Prevents default form submission behavior.

Validates required fields.

Disables the submit button and shows a "Sending..." status.

Calls addDoc() to save the contact data to the Firestore database.

On success, calls showMessage() to display a success modal and resets the form.

4. Modals (showMessage, showServiceDetail)

These utility functions manage custom modal dialogs, ensuring they:

Are visually centered and block the main page content (via the modal-base overlay).

Implement focus trapping (trapFocus() function) to meet accessibility standards, ensuring keyboard users cannot tab outside the modal content while it is visible.

Restore focus to the previously active element upon closing (restoreFocus() function).
