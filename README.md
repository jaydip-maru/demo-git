## This is a tutorial for How MERN Stack app initiateed.

1)Create -->Backend,
2)Create --> Frontend

Create a Two Folder in One Folder;

Step-1
Open a terminal and --> cd Backend
open a Secoend terminal and -> cd Frontend

step-2 --> For Backend

1) for initialize a backend
npm init -y

2)install Dependencys
npm i mongodb express cors dotenv

3)Create index.js file with this code
const express=require('express'),
http=require('http');
const hostname='localhost';
const port=8080;
const app=express();

app.use((req, res)=> {
        console.log(req.headers); 
        res.statusCode=200; 
        res.setHeader('Content-Type', 'text/html'); 
        res.end('<html><body><h1>This is a test server</h1></body></html>');
});
const sample_server=http.createServer(app);

sample_server.listen(port, hostname, ()=> {
        console.log(`Server running at http: //${hostname}:${port}/`);});

4)Change Package.json
Add into Script 
"start": "node index.js"
