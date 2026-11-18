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

