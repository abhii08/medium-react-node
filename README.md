# Application link:- 

# MEDIUM-BLOGGING

This is a full-stack Medium-like blogging platform built using modern web technologies. It includes features for user authentication, blog creation, editing, and viewing.
# Tech Stack
- React in the frontend  
- Cloudflare Workers in the backend  
- Zod as the validation library, type inference for the frontend types  
- TypeScript as the language  
- Prisma as the ORM, with connection pooling  
- Postgres as the database  
- JWT for authentication
  
## Project Structure

The project is organized into three main directories:

### 1. `backend`
  - **Runtime**: Cloudflare Workers (serverless)
  - **Framework**: Hono.js (lightweight web framework for Cloudflare Workers)
  - **Database**:
    - Prisma ORM (with Prisma Accelerate for edge compatibility)
    - PostgreSQL (database, referenced in Prisma schema)
  - **Authentication**: JWT (JSON Web Tokens)
  - **Validation**: Zod (via shared @abhinav08/medium-blogging package)
  - **Deployment**: Wrangler (Cloudflare Workers CLI)

### 2. `common`
   - **Validation**: Zod (for input validation)
   - **Type Sharing**: TypeScript types shared between frontend and backend

### 3. `frontend`
   - **Framework**: React 18 with TypeScript
   - **Build Tool**: Vite
   - **Styling**:
     - Tailwind CSS (utility-first CSS framework)
     - PostCSS (for processing Tailwind)
   - **Routing**: React Router v6
   - **HTTP Client**: Axios
   - **State Management**: React Hooks (useState, useEffect, custom hooks)
   - **Build Output**: Static files (SPA)

## Setup

To run the project locally:

#### 1. Clone the repository:
   ```bash
   git clone https://github.com/abhii08/MEDIUM-BLOGGING.git
   cd MEDIUM-BLOGGING
   ```
   
#### 2. Install dependencies for both frontend and backend:
```bash
cd backend
npm install
cd ../frontend
npm install
```

#### 3. Set up environment variables:
Create a .env file in the backend directory with the necessary variables (e.g., MongoDB URI, JWT secret).

#### 4. Run the backend server:
```bash
cd backend
npm run dev
```
#### 5. Run the frontend:
```bash
cd frontend
npm run dev
```

#### 6. Access the application at
```bash
http://localhost:3000
```
