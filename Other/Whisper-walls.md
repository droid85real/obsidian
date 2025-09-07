
- `main` → stable code only
- `dev` → all merged team work in progress
- `feature/...` → your personal sandbox for specific tasks

Folder structure
```
whisper-walls/
│
├── client/                      # React frontend
│   ├── public/
│   │   ├── index.html
│   │   └── favicon.ico
│   ├── src/
│   │   ├── App.js
│   │   ├── index.js
│   │   ├── App.css
│   │   └── components/          # Reusable UI components
│   ├── package.json
│   └── .gitignore
│
├── server/                      # Node/Express backend
│   ├── src/
│   │   ├── index.js              # Entry point
│   │   ├── routes/
│   │   │   └── example.routes.js # Example route
│   │   ├── controllers/
│   │   │   └── example.controller.js
│   │   └── config/
│   │       └── db.js             # DB connection setup (future)
│   ├── package.json
│   ├── .gitignore
│   └── .env
│
├── .gitignore                    # Root ignore (covers both client & server)
├── README.md
└── LICENSE

```


+ `git clone git@github.com:TechnoformX/whisper-walls.git` To clone github remote repo

## FRONTEND
+ inside whisper-walls 

```
mkdir client         # make new client folder
cd client            # go into it
npm create vite@latest
```
When Vite asks:
Project name: ./ (that means "this folder")
Framework: React
Variant: JavaScript 

```
npm install
npm run dev
```

#### **configure vite.config.js for cors**
```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

// https://vite.dev/config/
export default defineConfig({
  plugins: [react()],
  server:{
    proxy: {
      "/api":"http://localhost:5000",
    },
  },
})
```

Vite proxy handles CORS issues by forwarding /api calls from frontend to backend seamlessly during development.










---
## BACKEND
+ and inside server , `npm init` To initialise and then `npm i express` To install express
+ `npm i dotenv` for env support , and configure it `dotenv.config();`
+ `npm i cors`  allow frontend to call backend and configure it `server.use(cors());`



---

##### **Configuration to run both frontend and backend server at once**

STEP-1
+ In root run `npm i --save-dev concurrently`

STEP-2
+ update root `package.json`
```json
{
  "name": "whisper-walls",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "start": "concurrently \"npm run dev --prefix client\" \"npm start --prefix server\""
  },
  "devDependencies": {
    "concurrently": "^8.2.0"
  }
}
```

STEP-3
+ from root folder run `npm start` to see the output from both servers, and both will be running simultaneously

How this works
- `npm run dev --prefix client` runs your Vite dev server in the `client` folder.
- `npm start --prefix server` runs your Express server in the `server` folder (make sure `server/package.json` has `"start": "node index.js"` or equivalent).
- `concurrently` runs both commands **at the same time** in one terminal window.