# 🌀 Hono + Cloudflare Workers Backend

This repository contains the backend setup for a modern web application built using **[Hono](https://hono.dev/)**, **Cloudflare Workers**, and **Prisma ORM** with **PostgreSQL** (via Neon or Aiven) and **Prisma Accelerate** for connection pooling and optimized performance.

---

## 🚀 Step 1: Initialize the Backend

Start by creating a new Hono-based Cloudflare Worker application.

```bash
npm create hono@latest
```

**Configuration details:**

*   **Target directory:** backend
    
*   **Template:** cloudflare-workers
    
*   **Install dependencies:** yes
    
*   **Package manager:** npm
    

This will scaffold a Hono Cloudflare Worker app inside the backend directory.

⚙️ Step 2: Initialize Route Handlers
------------------------------------

For the initial version, we’ll define the following API routes:

### **User Routes**

*   POST /api/v1/user/signup – Register a new user
    
*   POST /api/v1/user/signin – Authenticate an existing user
    

### **Blog Routes**

*   POST /api/v1/blog – Create a new blog post
    
*   PUT /api/v1/blog – Update an existing blog post
    
*   GET /api/v1/blog/:id – Get a specific blog post by ID
    
*   GET /api/v1/blog/bulk – Retrieve multiple blog posts
    

🗄️ Step 3: Initialize the Database with Prisma
-----------------------------------------------

We’ll use **Prisma ORM** with a **PostgreSQL** database hosted on Neon or Aiven.

### 1️⃣ Get your Database Connection URL

Example:

Plain 
```bash
postgres://avnadmin:password@host/db   
```

### 2️⃣ Get a Connection Pool URL from Prisma Accelerate

From [Prisma Data Platform → Accelerate](https://www.prisma.io/data-platform/accelerate), you’ll get a connection pool URL similar to:

```bash
prisma://accelerate.prisma-data.net/?api_key=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpX...   
```
🧩 Step 4: Set Up Prisma in Your Project
----------------------------------------

Make sure you are in the backend folder, then install and initialize Prisma:

```bash
npm i prisma  npx prisma init   
```
### Update .env

Replace the DATABASE\_URL with your PostgreSQL connection string:

```bash
DATABASE_URL="postgres://avnadmin:password@host/db"   
```

🧾 Step 5: Configure Wrangler (Cloudflare)
------------------------------------------

In your wrangler.toml, add your Prisma Accelerate connection pool URL as a variable.

```bash
name = "backend"  compatibility_date = "2023-12-01"  [vars]  DATABASE_URL = "prisma://accelerate.prisma-data.net/?api_key=eyJhbGciOi..."   
```
🛠️ Step 6: Initialize and Migrate the Schema
---------------------------------------------

Run the following commands to set up your Prisma schema and generate the client:

```bash
npx prisma migrate dev --name init_schema  npx prisma generate --no-engine   
```
⚡ Step 7: Enable Prisma Accelerate Extension
--------------------------------------------

Install the Prisma Accelerate extension:

```bash
npm install @prisma/extension-accelerate   
```
Then initialize Prisma with Accelerate in your project:

```bash
import { PrismaClient } from '@prisma/client/edge'  import { withAccelerate } from '@prisma/extension-accelerate'  const prisma = new PrismaClient({    datasourceUrl: env.DATABASE_URL,  }).$extends(withAccelerate())
``` 
