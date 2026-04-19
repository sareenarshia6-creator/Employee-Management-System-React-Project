# 👨‍💼 Employee Management System
**A functional, frontend-focused React.js application designed to manage employees, assign tasks, and track their progress through a role-based dashboard system.**

![React](https://img.shields.io/badge/React-18.x-blue)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC)
![Vite](https://img.shields.io/badge/Vite-Bundler-purple)
![Context API](https://img.shields.io/badge/Context_API-State_Management-orange)

---

## 📝 Project Overview

The **Employee Management System (EMS)** is an industry-grade frontend project built using React.js. It focuses on separating concerns between administrative users and standard employees. 

Unlike standard to-do lists, this project handles complex user authentication (frontend simulation), role-based routing, Context API state management, and persistent data storage entirely within the browser. The application allows admins to assign tasks to specific employees while employees can accept, track, and complete their assigned tasks.

### Key Features & Architecture:
* **Role-Based Authentication:** Distinct login flows and dynamic routing for `Admin` and `Employee` accounts.
* **Admin Dashboard:** Enables admins to view all employees, track overall task statistics, and dynamically assign new tasks.
* **Employee Dashboard:** Enables employees to view their personalized task counts and manage their specific tasks via swipeable interactive cards.
* **Centralized State Management:** Utilizes React's Context API to seamlessly pass data between deeply nested components without prop drilling.
* **Persistent Browser Storage:** Utilizes the browser's `localStorage` to simulate a database, ensuring data (users, tasks, statuses) persists across page reloads.

## 💻 Tech Stack & Dependencies

**Core Framework & Bundler:**
* **React 18.x**: The core library used for building interactive, component-driven UI.
* **Vite**: Used as the lightning-fast frontend build tool and development server.

**Styling & UI:**
* **Tailwind CSS 3.x**: A utility-first CSS framework used to build highly responsive, modern, and clean UI components directly within JSX.

**State Management & Data:**
* **React Context API (`createContext`, `useContext`)**: Employed to create an `AuthProvider` that centrally manages the currently logged-in user and the global employee data state.
* **Local Storage API**: Native browser API used as a mock backend to store user credentials, task arrays, and task status updates permanently in the user's browser via JSON stringification and parsing.


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
## 📊 Local Storage Data Structure

Since there is no traditional backend database, the application relies on structured JSON data saved in the browser's Local Storage. 

| Key / Property | Description |
| :--- | :--- |
| `id` | Unique identification number for the employee |
| `firstName` | The employee's display name |
| `email` | Used alongside the password for authentication |
| `password` | The simulated password for login validation |
| `tasks` | An array of task objects containing `taskTitle`, `taskDescription`, `taskDate`, `category`, and boolean status flags (`active`, `newTask`, `completed`, `failed`) |
| `taskCounts` | An object tracking the numerical tally of the employee's current task statuses |

## ⚙️ Detailed Workflow & Steps

### 1. Project Setup & Styling
Before writing logic, the core architecture and UI components were established.
* **App Initialization:** Scaffolded the project using `npm create vite@latest` selecting React + JavaScript.
* **Component Architecture:** Divided the UI into modular folders (`Auth`, `Dashboard`, `TaskList`, `others`) to maintain a clean workspace.
* **Tailwind Integration:** Configured Tailwind CSS to handle styling directly within the components, avoiding messy external CSS files.

### 2. Authentication Flow & Local Storage Initialization
A robust mock backend was built to handle logins without a server.
* **Data Provisioning:** Built a helper file (`localStorage.jsx`) to seed default dummy data (5 employees and 1 admin) into `localStorage` using `JSON.stringify` upon initial load.
* **Two-Way Binding:** The `Login.jsx` component uses React's `useState` to capture email and password inputs in real-time.
* **Validation:** Upon form submission, `App.jsx` evaluates the credentials. If matched, it sets a `loggedInUserData` state and renders the respective dashboard.

### 3. Context API Implementation
Data needed to be accessible across the entire application without passing props down multiple levels.
* **Auth Provider:** Created `AuthProvider.jsx` to wrap the entire application component tree inside `main.jsx`.
* **Global Access:** Extracted employee data from Local Storage, parsed it, and provided it globally. Any component can now call `useContext(AuthContext)` to read or update user data.

### 4. Admin Dashboard Execution
The central hub for assigning work.
* **Task Creation Form:** Built `CreateTask.jsx` to capture new task details (title, description, date, category, assignee). 
* **State Mutation:** When a task is created, the application finds the specific employee in the global array, pushes the new task object into their `tasks` list, increments their "New Task" counter, and pushes the updated array back to `localStorage`.
* **Live Monitoring:** Built `AllTasks.jsx` to map through the Context API data and display a live summary of all employees and their current progress.

### 5. Employee Dashboard Execution
The personalized workspace for individual workers.
* **Task Statistics:** The `TaskListNumbers.jsx` component dynamically displays the tally of the logged-in employee's tasks.
* **Conditional Task Rendering:** The `TaskList.jsx` component maps through the user's specific `tasks` array. Using `if/else` logic based on task boolean flags (`active`, `newTask`, etc.), it dynamically renders the appropriate UI card (`NewTask`, `AcceptTask`, `CompleteTask`).

## 🚀 How to Run

1. Clone the repository to your local machine:
   ```bash
   git clone [https://github.com/your-username/employee-management-system.git](https://github.com/your-username/employee-management-system.git)
   cd employee-management-system
   ```

2. Install the required Node.js dependencies:
   ```bash
   npm install
   ```

3. Start the Vite development server:
   ```bash
   npm run dev
   ```

4. Open your browser and navigate to the local host address provided in the terminal (usually `http://localhost:5173`). 

   *Tip: Check your browser's Developer Tools -> Application -> Local Storage to view the dummy login credentials that are auto-generated on the first load to test the login system.*

## 📈 Future Improvements

- [ ] **Backend Integration:** Replace the Local Storage mock backend with a real database (e.g., MongoDB) and a Node.js/Express API for secure authentication and data persistence.
- [ ] **Dynamic Status Buttons:** Implement the `onClick` functionality on the Employee dashboard cards allowing users to actually click "Mark as Completed", directly updating the global state.
- [ ] **Admin Member Creation:** Add a specialized panel for Admins to register new employees dynamically from the UI.
- [ ] **Toast Notifications:** Integrate a library like `react-toastify` to provide better UX feedback during invalid login attempts or successful task creations.

