# MERN Stack Blog Application - Setup Guide

## 📋 Prerequisites

Before starting, make sure you have these installed:
- **Node.js** (version 18 or higher) - [Download here](https://nodejs.org/)
- **VS Code** - [Download here](https://code.visualstudio.com/)
- **Git** - [Download here](https://git-scm.com/)

## 🗂️ Project Structure

Your project should be organized like this in VS Code:

```
mern-blog/
├── client/                 # React frontend
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   │   └── api.js     # Your API service file
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
├── server/                 # Express backend
│   ├── models/
│   │   └── Post.js        # Your Post model
│   ├── routes/
│   ├── middleware/
│   ├── server.js          # Your server file
│   └── package.json
├── .env                   # Environment variables
└── README.md
```

## 🚀 Step-by-Step Setup

### Step 1: Create Project Structure

1. Open VS Code
2. Create a new folder called `mern-blog`
3. Open this folder in VS Code (File → Open Folder)
4. Create the following folder structure:
   - Create `client` folder
   - Create `server` folder
   - Inside `client`: create `src` folder
   - Inside `server`: create `models`, `routes`, `middleware` folders

### Step 2: Set Up the Server

1. Open terminal in VS Code (Terminal → New Terminal)
2. Navigate to server folder:
   ```bash
   cd server
   ```
3. Initialize npm:
   ```bash
   npm init -y
   ```
4. Install server dependencies:
   ```bash
   npm install express mongoose cors dotenv bcryptjs jsonwebtoken joi multer helmet express-rate-limit
   npm install -D nodemon
   ```

### Step 3: Set Up the Client

1. In terminal, go back to root and navigate to client:
   ```bash
   cd ../client
   ```
2. Create React app with Vite:
   ```bash
   npm create vite@latest . -- --template react
   ```
3. Install additional client dependencies:
   ```bash
   npm install axios react-router-dom lucide-react
   npm install -D tailwindcss postcss autoprefixer
   ```
4. Initialize Tailwind CSS:
   ```bash
   npx tailwindcss init -p
   ```

### Step 4: Database Setup (MongoDB)

You have two options:

#### Option A: MongoDB Atlas (Recommended for beginners)
1. Go to [MongoDB Atlas](https://www.mongodb.com/atlas)
2. Create a free account
3. Create a new cluster
4. Get your connection string

#### Option B: Local MongoDB
1. Download and install [MongoDB Community Server](https://www.mongodb.com/try/download/community)
2. Start MongoDB service
3. Use connection string: `mongodb://localhost:27017/mern-blog`

### Step 5: Environment Variables

Create a `.env` file in the root directory:

```env
# Server Configuration
PORT=5000
NODE_ENV=development

# Database Configuration
MONGODB_URI=your-mongodb-connection-string-here

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here
JWT_EXPIRES_IN=7d

# File Upload Configuration
MAX_FILE_SIZE=5000000
UPLOAD_PATH=uploads/
```

## 📁 File Setup

### Place Your Files

1. **Server files:**
   - Put your `server.js` in the `server/` folder
   - Put your `Post.js` in the `server/models/` folder

2. **Client files:**
   - Put your `api.js` in the `client/src/services/` folder

### Update Package.json Files

**Root package.json:**
```json
{
  "name": "mern-blog",
  "scripts": {
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "server": "cd server && npm run dev",
    "client": "cd client && npm run dev"
  },
  "devDependencies": {
    "concurrently": "^8.2.2"
  }
}
```

**Server package.json scripts:**
```json
{
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  }
}
```

## 🔧 Configuration Files

### Vite Config (client/vite.config.js)
```javascript
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:5000',
        changeOrigin: true,
      },
    },
  },
})
```

### Tailwind Config (client/tailwind.config.js)
```javascript
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

## 🏃‍♂️ Running the Application

### Method 1: Run Both Together (Recommended)
From the root directory:
```bash
npm install
npm run dev
```

### Method 2: Run Separately
**Terminal 1 (Server):**
```bash
cd server
npm run dev
```

**Terminal 2 (Client):**
```bash
cd client
npm run dev
```

## 🌐 Access Your Application

- **Frontend:** http://localhost:5173
- **Backend API:** http://localhost:5000
- **API Health Check:** http://localhost:5000/api/health

## 🔍 Troubleshooting

### Common Issues:

1. **MongoDB Connection Error:**
   - Make sure MongoDB is running (if local)
   - Check your connection string in `.env`
   - Ensure your IP is whitelisted (if using Atlas)

2. **Port Already in Use:**
   - Change the PORT in your `.env` file
   - Or kill the process using the port

3. **Module Not Found:**
   - Make sure you're in the correct directory
   - Run `npm install` in both client and server folders

4. **CORS Errors:**
   - Check your CORS configuration in server.js
   - Ensure the client URL is correct

## 📝 Next Steps

1. Create your React components in `client/src/components/`
2. Create your API routes in `server/routes/`
3. Add more models in `server/models/`
4. Style your components with Tailwind CSS

## 🆘 Getting Help

If you encounter issues:
1. Check the browser console for errors
2. Check the server terminal for error messages
3. Verify all dependencies are installed
4. Make sure all file paths are correct

Good luck with your MERN stack blog application! 🚀