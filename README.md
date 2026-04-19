# Employee-Management-System-React-Project


```markdown
# 👨‍💼 Employee Management System

**A functional, frontend-focused React.js application designed to manage employees, assign tasks, and track their progress through a role-based dashboard system.**

![React](https://img.shields.io/badge/React-18.x-blue)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC)
![Vite](https://img.shields.io/badge/Vite-Bundler-purple)
![Context API](https://img.shields.io/badge/Context_API-State_Management-orange)

---

## 📝 Project Overview

The **Employee Management System (EMS)** is an industry-grade frontend project built using React.js. It focuses on separating concerns between administrative users and standard employees. Through dynamic state management and Local Storage integration, the application allows admins to assign tasks to specific employees while employees can accept, track, and complete their assigned tasks.

Unlike standard to-do lists, this project handles complex user authentication (frontend simulation), role-based routing, Context API state management, and persistent data storage entirely within the browser.

### Key Features:
* **Role-Based Authentication:** Distinct login flows and dashboards for `Admin` and `Employee` accounts.
* **Admin Dashboard:** Admins can view all employees, track overall task statistics (New, Active, Completed, Failed), and create/assign new tasks dynamically.
* **Employee Dashboard:** Employees can view their personalized task counts and manage their specific tasks via swipeable interactive cards.
* **Task Lifecycle:** Tasks have distinct states (New, Accepted, Completed, Failed) that are updated via UI interactions.
* **Persistent Storage:** Utilizes the browser's `localStorage` to simulate a database, ensuring data persists across page reloads.
* **Context API:** Centralized state management to seamlessly pass data between nested components without prop drilling.

## 💻 Tech Stack & Dependencies

**Core Framework & Bundler:**
* **React 18.x**: The core library used for building interactive UI components.
* **Vite**: Used as the lightning-fast frontend build tool and development server.

**Styling & UI:**
* **Tailwind CSS 3.x**: A utility-first CSS framework used for highly responsive, modern, and rapid UI styling.

**State Management & Data:**
* **React Context API**: Employed to create an `AuthProvider` that centrally manages the currently logged-in user and the global employee data state.
* **Local Storage API**: Native browser API used as a mock backend to store user credentials, task arrays, and task status updates permanently in the user's browser.

## 📂 Project Structure

A clean, component-driven folder structure is maintained for scalability:

```text
src/
├── components/
│   ├── Auth/
│   │   └── Login.jsx           # Handles authentication UI and logic
│   ├── Dashboard/
│   │   ├── AdminDashboard.jsx  # Admin view
│   │   └── EmployeeDashboard.jsx # Employee view
│   ├── TaskList/               # Task card variations
│   │   ├── AcceptTask.jsx
│   │   ├── CompleteTask.jsx
│   │   ├── FailedTask.jsx
│   │   └── NewTask.jsx
│   └── others/
│       ├── Header.jsx          # Top navigation and logout
│       ├── CreateTask.jsx      # Admin task creation form
│       ├── AllTasks.jsx        # Admin view of all employee tasks
│       └── TaskListNumbers.jsx # Stats cards (counters)
├── context/
│   └── AuthProvider.jsx        # Context API for global state
├── utils/
│   └── localStorage.jsx        # Helper functions to get/set local storage data
├── App.jsx                     # Main routing and auth-check logic
└── main.jsx                    # Application entry point wrapped in AuthProvider
```

## ⚙️ Detailed Workflow & Architecture

### 1. Project Setup & Styling
* Initialized via `npm create vite@latest` selecting React + JavaScript.
* Integrated `Tailwind CSS` by configuring `tailwind.config.js` and importing base directives into `index.css`.

### 2. Authentication Flow & Local Storage Initialization
* Built a robust mock backend using `localStorage.jsx`. Upon initial load, it provisions default dummy data (5 employees and 1 admin) using `JSON.stringify`.
* The `Login.jsx` component uses two-way data binding (React `useState`) to capture the email and password.
* Upon submission (`onSubmit`), `App.jsx` evaluates the credentials against the Local Storage data. If matched, it sets the `loggedInUserData` state and redirects the user to their respective dashboard.

### 3. Context API Implementation
* Created `AuthProvider.jsx` to wrap the entire `<App />` component inside `main.jsx`.
* Extracted employee data from Local Storage, parsed it, and provided it globally via `AuthContext.Provider`.
* This eliminates prop drilling, allowing deeply nested components (like `Header` or `AllTasks`) to directly consume user data.

### 4. Admin Dashboard Execution
* **Task Creation (`CreateTask.jsx`):** A controlled form that captures task title, description, date, category, and the assigned employee. Upon submission, it constructs a new task object.
* **Data Mutation:** The application locates the specific employee in the global array, pushes the newly created task object into their `tasks` array, increments their specific "New Task" counter, and updates `localStorage` using `JSON.stringify()`.
* **Global View (`AllTasks.jsx`):** Maps through the Context API data to display a live summary of all employees and their respective task counts.

### 5. Employee Dashboard Execution
* **Task Statistics (`TaskListNumbers.jsx`):** Dynamically displays the count of the logged-in employee's tasks categorized by status (New, Active, Completed, Failed).
* **Task Rendering (`TaskList.jsx`):** Maps through the logged-in user's specific `tasks` array. Using conditional rendering (`if/else` logic based on task boolean flags like `active`, `newTask`, etc.), it renders the appropriate component card (`NewTask`, `AcceptTask`, etc.).

## 🚀 How to Run Locally

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/your-username/employee-management-system.git](https://github.com/your-username/employee-management-system.git)
   cd employee-management-system
   ```

2. **Install dependencies:**
   Ensure you have Node.js installed, then run:
   ```bash
   npm install
   ```

3. **Start the development server:**
   ```bash
   npm run dev
   ```

4. **Access the application:**
   Open your browser and navigate to `http://localhost:5173`. 
   
   *Tip: Check your browser's Developer Tools -> Application -> Local Storage to view the dummy login credentials auto-generated on the first load.*

## 📈 Future Improvements

- [ ] **Backend Integration:** Replace Local Storage with a real database (e.g., MongoDB) and build a Node.js/Express backend for secure authentication and data persistence.
- [ ] **Dynamic Task Status Updates:** Implement functionality on the Employee dashboard allowing users to click "Mark as Completed" or "Accept", directly updating the boolean flags in the global state.
- [ ] **Admin Member Creation:** Add a panel for Admins to register new employees directly from the UI dynamically.
- [ ] **Toast Notifications:** Add libraries like `react-toastify` to provide better UX feedback during invalid logins or successful task creations.
```
