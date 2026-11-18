## This is a tutorial for How MERN Stack app initiateed.

1)Create -->Backend,
2)Create --> Frontend

Create a Two Folder in One Folder;

Step-1
Open a terminal and --> cd Backend
open a Secoend terminal and -> cd Frontend

step-2 --> For Backend

1) for initialize a backend
 ```bash
npm init -y
```

2)install Dependencys
 ```bash
npm i mongodb express cors dotenv
 ```

3)Create index.js file with this code
```JavaScript
import express from "express";
import cors from "cors";
import dotenv from "dotenv";

dotenv.config();

const app = express();

// Middleware
app.use(cors());
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Test route
app.get("/", (req, res) => {
    res.status(200).json({
        success: true,
        message: "Backend server is running!"
    });
});

// Server
const PORT = process.env.PORT || 5000;

app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```

4)Change Package.json
Add into Script 
"start": "node index.js"
->Change type
"type": "module"

Step-2 Frontend

1) For initialization
   ```
   npm create vite@latest .
   ```
   Select configuration
Choose:
- Framework: React
- Variant: JavaScript
- Linter: ESLint
  this is for instalation
```
npm i
```

2) Start a Reat app
   ```
   npm run dev
   ```
3)Add this code into a APP.jsx
this connect your front end with backend
```
import axios from "axios";
import { useEffect } from "react";

function App() {
    useEffect(() => {
        axios.get("http://localhost:5000")
            .then(res => console.log(res.data))
            .catch(err => console.log(err));
    }, []);

    return <h1>React Frontend Connected!</h1>;
}

export default App;
```
Step-3 Curd operation

Backend
1)Controler
```
import User from "../models/User.js";

// CREATE USER
export const createUser = async (req, res) => {
    try {
        const { name, email, age } = req.body;

        const user = await User.create({
            name,
            email,
            age
        });

        res.status(201).json({
            success: true,
            user
        });

    } catch (error) {
        res.status(500).json({
            success: false,
            message: error.message
        });
    }
};

// GET ALL USERS
export const getUsers = async (req, res) => {
    try {
        const users = await User.find();

        res.status(200).json({
            success: true,
            users
        });

    } catch (error) {
        res.status(500).json({
            success: false,
            message: error.message
        });
    }
};

// UPDATE USER
export const updateUser = async (req, res) => {
    try {
        const user = await User.findByIdAndUpdate(
            req.params.id,
            req.body,
            { new: true, runValidators: true }
        );

        if (!user) {
            return res.status(404).json({
                success: false,
                message: "User not found"
            });
        }

        res.status(200).json({
            success: true,
            user
        });

    } catch (error) {
        res.status(500).json({
            success: false,
            message: error.message
        });
    }
};

// DELETE USER
export const deleteUser = async (req, res) => {
    try {
        const user = await User.findByIdAndDelete(req.params.id);

        if (!user) {
            return res.status(404).json({
                success: false,
                message: "User not found"
            });
        }

        res.status(200).json({
            success: true,
            message: "User deleted successfully"
        });

    } catch (error) {
        res.status(500).json({
            success: false,
            message: error.message
        });
    }
};
```

2)Routes
```

import express from "express";

import {
    createUser,
    getUsers,
    updateUser,
    deleteUser
} from "../controllers/userController.js";

const router = express.Router();

router.post("/", createUser);
router.get("/", getUsers);
router.put("/:id", updateUser);
router.delete("/:id", deleteUser);

export default router;
```
3) Index.js
   app.use("/api/users", userRoutes);




Step-4 For Frontend

```
import { useEffect, useState } from "react";
import axios from "axios";

const API = "http://localhost:5000/api/users";

function App() {
    const [users, setUsers] = useState([]);

    const fetchUsers = async () => {
        try {
            const { data } = await axios.get(API);
            setUsers(data.users);
        } catch (error) {
            console.log(error);
        }
    };

    useEffect(() => {
        fetchUsers();
    }, []);

    return (
        <div>
            <h1>User Management</h1>

            {users.map((user) => (
                <div key={user._id}>
                    <h3>{user.name}</h3>
                    <p>{user.email}</p>
                    <p>{user.age}</p>
                </div>
            ))}
        </div>
    );
}

export default App;
```
