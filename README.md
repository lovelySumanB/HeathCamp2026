# Health Camp Registration System — Mini Project

A responsive, client-side web application built for the **Community Health & Wellness Camp 2026**. This project allows community members to explore camp medical services, register for appointments, receive verified registration passes with unique IDs, and provides healthcare administrators with a real-time dashboard for managing participants, tracking slot capacities, and viewing analytics.

---

## 1. Project Overview

The **Health Camp Registration System** is designed to replace paper-based health camp queues with a digital pre-registration system. It ensures optimal doctor-patient scheduling by limiting time-slot capacity, preventing duplicate registrations, and generating printable registration passes.

### Core Objectives:
* Present health camp information, schedule, services, and doctor profiles.
* Client-side multi-section registration form with real-time field validation.
* Unique sequential Registration ID generation (e.g., `HC2026-0001`).
* Instant appointment pass with print functionality (`window.print()`).
* Registration lookup by ID or 10-digit mobile number.
* Interactive Admin Dashboard with live KPI counters, service distributions, slot occupancy bars, search, filtering, and full CRUD capabilities.
* Persistent browser storage via the HTML5 `localStorage` API.

---

## 2. Technologies Used

Strictly adheres to frontend-only requirements without external JS frameworks, Node.js, or backend servers:

* **HTML5**: Semantic tags (`<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`).
* **CSS3**: Custom design system in `css/style.css`, CSS variables, media queries, and dedicated print stylesheet (`@media print`).
* **Vanilla JavaScript (ES6+)**: Modular code, arrow functions, template literals, array methods (`filter`, `map`, `reduce`), DOM manipulation, and JSON serialization.
* **Bootstrap 5.3.3**: Responsive grid layout, modals, badges, cards, navigation bar, alerts, and utility classes.
* **Bootstrap Icons 1.11.3**: Crisp iconography across services, status badges, and navigation.
* **Google Fonts**: Modern *Plus Jakarta Sans* typography.

---

## 3. Project Structure

```
health-camp-registration/
│
├── index.html            # Landing / Home page (Camp details, services, doctors, FAQs)
├── register.html         # Participant registration form & success modal
├── lookup.html           # Registration search & printable admit pass
├── admin.html            # Admin dashboard with statistics, filterable table & CRUD modals
│
├── css/
│   └── style.css         # Custom styling, medical palette tokens & print layout
│
└── js/
    ├── app.js            # Core engine: storage keys, ID generator, slot logic, demo data
    ├── registration.js   # Form validation, live slot counts, duplicate check & submit logic
    ├── lookup.js         # Search engine by ID/Mobile & admit pass renderer
    └── admin.js          # Live KPIs, multi-filter table, View/Edit/Delete modals, JSON export
```

---

## 4. Key Features

### A. Landing Page (`index.html`)
* **Hero Banner**: Call-to-actions ("Register Now", "View Camp Details"), quick statistics (100% Free, 8+ Services, 20+ Doctors).
* **Camp Details Card**: Date (Nov 15–17, 2026), Time (09:00 AM – 05:00 PM), Venue, Organizer info, Helpline.
* **8 Available Medical Services**:
  1. General Health Checkup
  2. Blood Pressure Check
  3. Blood Sugar Test
  4. BMI & Body Composition Analysis
  5. Comprehensive Eye Checkup
  6. Dental Checkup & Hygiene
  7. Nutrition & Diet Consultation
  8. Specialist Doctor Consultation
* **Medical Specialists**: Doctor profiles with qualifications and hospital affiliations.
* **4-Step Process Guide**: Clear participation roadmap.
* **FAQ Accordion & Emergency Notice**: Information on fasting guidelines, documents required, and emergency disclaimers.

### B. Registration Page (`register.html` & `registration.js`)
* **Personal Information**: Full Name, Date of Birth (max date = today), Age (auto-calculated from DOB), Gender, Mobile Number, Email, Residential Address, City, Emergency Contact (validated: cannot be identical to personal mobile).
* **Health Information**: Blood Group, Existing Medical Conditions, Allergies, Current Medications, Preferred Checkup, Specific Health Concerns.
* **Appointment Scheduling**:
  * Date selection (Nov 15, 16, or 17, 2026).
  * Dynamic time slots (09:00–10:00 AM, 10:00–11:00 AM, 11:00 AM–12:00 PM, 02:00–03:00 PM, 03:00–04:00 PM, 04:00–05:00 PM).
  * Slot capacity enforcement: Maximum 10 participants per slot. Displays remaining available slots and disables full slots with a `[SLOT FULL]` badge.
* **Consent Checkboxes**: Information accuracy declaration and privacy terms agreement.
* **Duplicate Prevention**: Rejects duplicate registrations for the same mobile number on the same date.
* **Success Modal**: Shows confirmed registration ID, participant summary, quick clipboard copy, and print button.

### C. Registration Lookup (`lookup.html` & `lookup.js`)
* Search by unique Registration ID (e.g. `HC2026-0001`) or 10-digit mobile number.
* Displays an official **Health Camp Admit Pass** with barcode simulation, participant details, and instructions.
* Print-friendly formatting that omits navbars and footers for clean printing.
* Direct URL query support (e.g., `lookup.html?id=HC2026-0001`).

### D. Admin Dashboard (`admin.html` & `admin.js`)
* **KPI Metric Cards**: Total Registrations, Today's Registrations, Male, Female, Confirmed, and Remaining Available Slots.
* **Visual Analytics**:
  * Service breakdown progress bars.
  * Slot occupancy indicators for appointment schedule tracking.
* **Search & Filter Controls**: Real-time filtering by keyword (Name/ID/Phone), Gender, Blood Group, Service, and Date.
* **Responsive Data Table**: Lists registrations with status badges (Registered, Confirmed, Completed, Cancelled).
* **Action Modals**:
  * **View Modal**: Full participant medical and appointment summary.
  * **Edit Modal**: Update participant details, slot, or status.
  * **Delete Modal**: Safe deletion with participant confirmation.
  * **Load Demo Data**: Injects 8 diverse sample registrations.
  * **Clear All Data**: Resets localStorage with confirmation prompt.
  * **Export Data**: Downloads registrations as a formatted `.json` file.

---

## 5. How LocalStorage is Used

The application uses the browser's `window.localStorage` under the key:
```javascript
const STORAGE_KEY = 'health_camp_registrations_2026';
```

### Data Schema Example:
```json
[
  {
    "id": "HC2026-0001",
    "fullName": "Eleanor Vance",
    "dateOfBirth": "1994-04-12",
    "age": 32,
    "gender": "Female",
    "mobile": "9876543210",
    "email": "eleanor.vance@example.com",
    "address": "42 Greenfield Lane, Apt 3B",
    "city": "Metro City",
    "emergencyContact": "9876543219",
    "bloodGroup": "O+",
    "medicalConditions": "None",
    "allergies": "Penicillin",
    "medications": "Multivitamins",
    "preferredCheckup": "General Health Checkup",
    "preferredDate": "2026-11-15",
    "preferredTime": "09:00 AM - 10:00 AM",
    "reason": "Annual general wellness & preventive screening",
    "status": "Confirmed",
    "registrationDate": "2026-10-01T09:30:00.000Z",
    "consent": true
  }
]
```

---

## 6. How to Run the Project

1. **Directly in Browser**:
   * Navigate to the project folder and double-click `index.html`.
   * The application runs locally using standard browser APIs without needing a web server.

2. **Using a Local Static Server (Optional)**:
   * Using Python (if installed):
     ```bash
     python -m http.server 8000
     ```
   * Or using VS Code Live Server extension: right-click `index.html` and choose **Open with Live Server**.

---

## 7. Viva / Demonstration Test Flows

| Flow | Steps to Demonstrate | Expected Result |
| :--- | :--- | :--- |
| **Flow 1: Registration** | Go to `register.html` &rarr; Enter DOB &rarr; Age auto-fills &rarr; Pick date & time slot &rarr; Submit. | Shows Success Modal with newly generated ID (`HC2026-XXXX`) and confirmed details. |
| **Flow 2: Lookup & Print** | Go to `lookup.html` &rarr; Click demo chip `ID: HC2026-0001` &rarr; Click Search. | Displays official admit pass with barcode simulation and click "Print Admit Pass". |
| **Flow 3: Admin Dashboard** | Go to `admin.html` &rarr; Click "Load Demo Data". | 8 sample participants populate, KPI cards update instantly, and progress bars reflect real data. |
| **Flow 4: Filter & Search** | In Admin, type a name in search bar or filter by Blood Group `O+`. | Table updates dynamically without page reload. |
| **Flow 5: Edit & Status** | Click "Edit" icon on any row &rarr; Change status to `Confirmed` &rarr; Save. | Table row badge updates to green Confirmed badge and KPI counter recalculates. |
| **Flow 6: Delete Record** | Click "Delete" icon on any row &rarr; Confirm deletion in modal. | Record removed from localStorage; table and counters refresh. |
| **Flow 7: Slot Capacity** | Register multiple participants in the same slot until count reaches 10. | The slot displays `[SLOT FULL]` and becomes disabled in the registration form. |
| **Flow 8: Duplicate Check** | Attempt to register with the same mobile number and appointment date. | Bootstrap warning alert flags existing registration ID and blocks submission. |
| **Flow 9: Refresh Persistence** | Register a participant &rarr; Refresh the browser page (`F5`). | All records remain intact in localStorage. |

---

## 8. Future Enhancements

* Integration with an SMS/WhatsApp gateway for automated confirmation messages.
* Generation of scannable QR codes encoding participant IDs.
* Multi-language support (English, Spanish, Hindi, regional languages).
* Doctor portal for recording diagnosis notes directly onto participant records during the camp.
