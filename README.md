# ENTNT Ship Maintenance Dashboard

This project is a frontend-only Ship Maintenance Dashboard developed for the ENTNT Technical Assignment. It simulates the management of ships, their components, and associated maintenance jobs using React, React Router, Context API for state management, and TailwindCSS for styling. All data interactions are handled via `localStorage`.

**Submission Deadline:** Monday, 2 June (as per assignment details)

## Deployed Application Link

*   **Link:** https://entnt-ship-maintenance-dashboard.vercel.app/
    *   *Note: You will need to deploy this project to a service like Vercel, Netlify, or GitHub Pages and replace this placeholder.*

## Features Implemented

*   **User Authentication (Simulated):**
    *   Hardcoded users (Admin, Inspector, Engineer).
    *   Login/Logout functionality.
    *   Session persistence with `localStorage`.
    *   Role-Based Access Control (RBAC) on the frontend.
*   **Ships Management:**
    *   List, Create, Edit, Delete Ships.
    *   Detailed Ship Profile page (General Info, Components Installed, Maintenance History).
*   **Ship Components Management:**
    *   Add, Edit, Delete Components (linked to Ships).
    *   View Component Details.
*   **Maintenance Jobs Management:**
    *   Create, Edit, Delete (Admin) Maintenance Jobs for Components.
    *   Update Job status.
    *   View and Filter Jobs (by Ship, Status, Priority).
*   **Maintenance Calendar:**
    *   Display scheduled jobs in a Monthly/Weekly/Daily calendar view.
    *   Clicking a date shows jobs for that day (in a modal).
    *   Clicking a job on the calendar opens its edit form.
*   **Notification Center:**
    *   In-app, dismissible notifications for key actions (Job Created/Updated, CRUD operations).
*   **KPIs Dashboard:**
    *   Displays: Total Ships, Components with Overdue Maintenance (basic check), Jobs in Progress/Completed.
    *   Uses cards and placeholder charts for visual representation.
*   **Data Persistence:**
    *   All data (users, ships, components, jobs, session) persists using `localStorage`.
*   **Responsive Design:**
    *   The application is designed to be responsive across mobile, tablet, and desktop devices using TailwindCSS.
*   **Form Validation:**
    *   Basic client-side form validation and user feedback.

## Tech Stack

*   **Core:** React 18 (Functional Components, Hooks)
*   **Routing:** React Router DOM v6
*   **State Management:** React Context API
*   **Styling:** TailwindCSS v3
*   **Calendar:** `react-big-calendar`
*   **Charts:** `recharts` (placeholders implemented, full integration for visual charts)
*   **Date Handling:** `date-fns`
*   **Unique IDs:** `uuid`
*   **Build Tool:** Vite

## Setup and Installation

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-link>
    cd entnt-ship-maintenance-dashboard
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```
    or
    ```bash
    yarn install
    ```

3.  **Run the development server:**
    ```bash
    npm run dev
    ```
    or
    ```bash
    yarn dev
    ```
    The application will typically be available at `http://localhost:5173` (or another port if 5173 is busy).

4.  **Build for production:**
    ```bash
    npm run build
    ```
    or
    ```bash
    yarn build
    ```
    This will create a `dist` folder with the production-ready static assets.

## Application Architecture Overview

*   **`src/`**: Main source code directory.
    *   **`App.jsx`**: Main application component, sets up routing.
    *   **`main.jsx`**: Entry point, renders App, sets up Context Providers and Router.
    *   **`components/`**: Reusable UI components.
        *   **`Auth/`**: Authentication related components (e.g., `LoginForm.jsx` - though login is a page here).
        *   **`Dashboard/`**: Components for the KPI dashboard (e.g., `KPICard.jsx`).
        *   **`Layout/`**: Structural components like `Navbar.jsx`, `Sidebar.jsx`, `MainLayout.jsx`.
        *   **`Ships/`**, **`Components/`**, **`Jobs/`**: Components specific to managing these entities (Forms, Lists, ListItems).
        *   **`Notifications/`**: `NotificationCenter.jsx` for displaying alerts.
        *   **`UI/`**: Generic UI elements like `Modal.jsx`, `Button.jsx`, `InputField.jsx`, `ProtectedRoute.jsx`.
    *   **`contexts/`**: React Context API providers for global state.
        *   **`AuthContext.jsx`**: Manages user authentication state and session.
        *   **`DataContext.jsx`**: Manages data for ships, components, and jobs, including CRUD operations and `localStorage` interaction.
        *   **`NotificationContext.jsx`**: Manages system-wide notifications.
    *   **`hooks/`**: Custom React Hooks (not extensively used in this version but a good place for them).
    *   **`pages/`**: Top-level components for each route/view (e.g., `LoginPage.jsx`, `DashboardPage.jsx`).
    *   **`services/`**: Service modules, primarily `localStorageService.js` for all `localStorage` interactions and initial data seeding.
    *   **`styles/`**: Global styles (`main.css` including Tailwind directives).
    *   **`utils/`**: Utility functions (`helpers.js` for date formatting, `roleUtils.js` for RBAC checks).
    *   **`config/`**: Configuration files, like `initialData.js`.

## Data Model Overview (Simplified for localStorage)

*   **User:** `id`, `role` (Admin, Inspector, Engineer), `email`, `password` (simulated).
*   **Ship:** `id`, `name`, `imo`, `flag`, `status`.
*   **Component:** `id`, `shipId`, `name`, `serialNumber`, `installDate`, `lastMaintenanceDate`.
*   **Job:** `id`, `componentId`, `shipId`, `type`, `priority`, `status`, `assignedEngineerId`, `scheduledDate`, `description`, `completionDate` (optional).
*   **Notification:** `id`, `message`, `type`.
*   **Session:** `currentUser` (object), `token` (simulated).

All data is stored as JSON strings in `localStorage`.

## Technical Decisions Made

*   **React Context API for State Management:** Chosen for its built-in nature with React and suitability for the scale of this application, avoiding the need for an external library like Redux for this particular assignment.
*   **TailwindCSS for Styling:** Selected for rapid UI development and its utility-first approach, making responsiveness easier to implement.
*   **`localStorage` for Data Persistence:** As per assignment requirements. A `localStorageService.js` abstracts these interactions.
*   **Functional Components and Hooks:** Adhering to modern React best practices.
*   **Vite for Build Tool:** For its fast development server and build times.
*   **`react-big-calendar`:** A robust library for calendar functionality.
*   **`recharts` (Placeholder):** A popular charting library for React. Basic placeholders are used, full chart implementation would involve more detailed data mapping.
*   **Modular Structure:** The project is organized into features (ships, components, jobs) and common concerns (UI, layout, contexts) to promote maintainability.

## Known Issues or Limitations

*   **Security:** `localStorage` is not secure for sensitive data. Passwords are hardcoded and checked client-side, which is purely for simulation and **NOT secure for real applications**.
*   **Data Integrity:** No complex validation or relational integrity checks that a backend database would provide. Deleting a ship also deletes its components and jobs by iterating; more robust solutions would be needed in a real system.
*   **Scalability:** `localStorage` has size limits and performance can degrade with very large datasets.
*   **Error Handling:** Basic error handling is in place. More comprehensive error boundaries and user feedback could be added.
*   **Loading States:** Basic loading states are implemented. More granular loading indicators could improve UX.
*   **Charts:** Chart components are placeholders. Full integration with `recharts` would require more specific data transformation and chart configuration.
*   **Overdue Maintenance Logic:** The "Components with Overdue Maintenance" KPI uses a very basic date comparison. Real-world scenarios would likely involve more complex rules (e.g., maintenance intervals).
*   **Real-time Updates:** No real-time collaboration features; data is local to the browser.

## Bonus Features

*   None explicitly implemented beyond the core requirements due to time/scope constraints. Potential bonuses like dark mode or report exports are not included.

---

*This project was created based on the technical assignment PDF for ENTNT.*