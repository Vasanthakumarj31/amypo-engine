# AMYPO Interactive Coding Platform

AMYPO is a full-stack, interactive learning platform designed for teaching and practicing frontend web development (HTML, CSS, and JavaScript). It features a real-time coding workspace, an advanced automated evaluation engine, and a comprehensive dashboard for both students and trainers.

## 🚀 Key Features

### Student Experience
- **Interactive Workspace**: A split-pane coding environment featuring an integrated code editor and live live-preview.
- **Real-Time Automated Evaluation**: Code is evaluated securely on the backend. The evaluator checks HTML structure (DOM analysis), CSS styling logic, and runs JavaScript to verify interactive output.
- **Visual Regression Testing**: Student outputs are captured as screenshots and visually compared against trainer-provided reference images using pixel-matching algorithms.
- **Dashboard & Progression**: Students can track their progress across different courses, levels, and specific frontend coding challenges.

### Trainer & Admin Experience
- **Curriculum Management**: Trainers can define custom lessons, coding challenges, and expected outputs.
- **Material Overrides**: Trainers can upload starter code (HTML, CSS, JS) and reference images for specific lessons, overriding default content.
- **Student Tracking**: Trainers can monitor student progress and view their specific code submissions and evaluation scores.

## 🛠️ Technology Stack & Tools Used

### Frontend (Client)
- **[React 18](https://react.dev/) & [Vite](https://vitejs.dev/)**: Fast, modern frontend framework and build tool.
- **[TypeScript](https://www.typescriptlang.org/)**: For strict type safety across the entire codebase.
- **[Monaco Editor](https://microsoft.github.io/monaco-editor/)** (`@monaco-editor/react`): The core editor powering the interactive workspace (same engine as VS Code).
- **[Tailwind CSS](https://tailwindcss.com/) & [Shadcn UI](https://ui.shadcn.com/)**: For rapid, accessible, and beautifully designed user interfaces. Built on top of Radix UI primitives.
- **[Framer Motion](https://www.framer.com/motion/)**: Smooth, physics-based UI animations and page transitions.
- **[React Resizable Panels](https://github.com/bvaughn/react-resizable-panels)**: Provides the draggable, resizable split-pane layout in the coding workspace.
- **[Lucide React](https://lucide.dev/)**: Clean, modern icon set.

### Backend (Server)
- **[Node.js](https://nodejs.org/) & [Express](https://expressjs.com/)**: Fast unopinionated backend web framework.
- **[Puppeteer](https://pptr.dev/)**: Headless Chrome Node.js API. Used to render the student's code in a real headless browser context, capture screenshots, and query the resulting DOM tree.
- **[Pixelmatch](https://github.com/mapbox/pixelmatch) & [PNGJS](https://github.com/lukeapage/pngjs)**: Image comparison libraries. Used to diff the headless browser screenshots against the trainer's reference images and calculate a visual accuracy percentage.
- **[MongoDB] & [Mongoose](https://mongoosejs.com/)**: NoSQL database for flexible data modeling of curriculums, user progress, and code submissions.
- **[MongoDB Memory Server](https://github.com/nodkz/mongodb-memory-server)**: Spins up a real, local MongoDB instance in memory for fast, zero-config local development and testing.

## 🏃‍♂️ Getting Started

### Prerequisites
Make sure you have Node.js and npm (or pnpm/yarn) installed. 

### Running Locally

1. **Start the backend server:**
   ```bash
   cd server
   npm install
   npm run dev
   ```
   *(The server runs on port 5000 and uses an in-memory MongoDB instance by default).*

2. **Start the frontend client:**
   Open a new terminal window:
   ```bash
   npm install
   npm run dev
   ```
   *(The application will be accessible at `http://localhost:8080`)*

---

## 🔄 Application Workflow

### 1. Trainer Course Management
- **Dashboard Overview**: Trainers start at their dashboard ( `/trainer` ) to get a high-level view of student progress, total submissions, and average evaluation scores.
- **Curriculum Definition**: In the *Curriculum Manager*, trainers create and structure courses divided into specific levels and lessons.
- **Problem Creation**: Trainers create specific coding challenges. For each challenge, they define:
  - The goal/description.
  - Expected output conditions.
  - Optional starter HTML/CSS/JS code to give students a baseline.
  - An uploaded Reference Image (how the end result should look visually).

### 2. Student Learning & Coding
- **Course Selection**: Students log in and view their assigned courses and progress on the main dashboard (`/dashboard`).
- **Workspace Navigation**: When a student selects a lesson/problem, they are taken to the Interactive Workspace (`/workspace/:id`).
- **Coding**: The workspace provides a 3-tab code editor (HTML, CSS, JS) on the left, and a live updating visual preview on the right. 
- **Reference View**: Students can toggle the "Reference Image" panel to see exactly what they need to build.

### 3. Submission & Automated Evaluation
- **Executing Code**: Once finished, students hit the "Submit" or "Evaluate" button.
- **Backend Rendering**: The server takes the student's code bundle and spins up an isolated Headless Chrome Browser instance using Puppeteer.
- **Evaluation Pipeline**:
  - **DOM Tests**: The server inspects the rendered DOM tree to check if required elements (e.g., specific tags, classes) are present.
  - **CSS Tests**: It verifies computed styles against expectations.
  - **JS Tests**: It looks for expected console output and runtime errors.
  - **Visual Diff**: The server takes a PNG screenshot of the student's rendered page and does a strict pixel-by-pixel comparison using `pixelmatch` against the trainer's reference image.
- **Feedback Loop**: Results and detailed feedback (what passed/failed) are sent back to the student's Workspace instantly, along with an overall percentage score.

### 4. Progress Tracking
- **Student Stats**: Passing a challenge marks the lesson as "Complete", updating the student's personal progress bars on their dashboard.
- **Trainer Analytics**: Trainers can review all student submissions, see exactly which tests students are struggling with, and adjust curriculum accordingly.

---
*Built for modern frontend education with automated precision.*
