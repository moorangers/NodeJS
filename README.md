# NodeJS
Node.js is a JavaScript runtime environment that runs on the V8 engine. It executes JavaScript code outside a web browser.

We can execute a JavaScript file using Node.js with the CLI command node <js_file_path>.

## File System
fs Module: fs stand for "File System" is module in Node.js and use manage file in computer.
 -  `reading file => fs.readFile("fillepath", function)`
 -  `Write file (OverWrite) => fs.writeFile("fillepath", function)`
 -  `Write append data onto existing file => fs.appendFile("fillepath", function)`
 -  `Delete file => unlinkFile("fillepath", function)`
 -  `In Node.js, we use .catch to handle errors in promises.` 
 -  `In Node.js, we use try ... catch to handle errors with the await keyword.`

## API
### HTTP Request Method 
  -  `GET => for Created`
  -  `POST => for Add`
  -  `PUT => for Updated`
  -  `DELETE => for Deleted`
    
### Creating API Routes.
  - `app.method(path, handler)`
    - `app` is Express Object
    - `method` is HTTP Request Method เช่น `get`, `post`, `put`, `delete`
    - `path` is API Endpoint บน Server เช่น `/posts`
    - `handler` is Controller ที่จะทำงานเมื่อ Request วิ่งเข้ามาตาม Route ที่กำหนด
### Returning Responses.
  - `ใน Express เราสามารถสร้าง Response ได้ด้วย Object res.send()`
  - `ใน Express เราสามารถสร้าง Response กลับเป็น JSON ได้ด้วย res.json() ซึ่งรับ Input เป็น JavaScript Objec`
  
## Express
- Creating Server Applications with Express

    Start: npm install express
      
       import express from "express";

       const app = express();
       const port = 4000;

- app.get เพื่อสร้าง API Route มาทดสอบ ซึ่งเป็น Method ที่รับ Input 2 ตัว <"Endpoint">, <Callback Function ซึ่งเรียกว่า Controller>

        app.get('/', (req, res) => {
          res.send('Konichiwa DTs')
        });
      
- app.listen เป็น Method ที่รับ Input 2 ตัว ได้แค่ port, callback Function ที่ทำงานหลังจาก server ถูกเปิดใช้
  
         app.listen(port, () => {
          console.log(`Server is running at ${port}`)
        });

## Router
### Using Express Router

##### โค้ดนี้อยู่ในไฟล์ apps/memberRouter.js

Import ตัว "Router" ด้วย Named Import จาก "express"
        
        import { Router } from "express";

Initialize ตัว Router ขึ้นมาด้วย Router()
        
        const memberRouter = Router();

ใช้ router.method(path, handler) ในการสร้าง Routes แทน app.method(path, handler)
 
        memberRouter.get('/', function (req, res) {
          res.send('Got a GET /members Request');
        });
        memberRouter.get('/:id', function (req, res) {
          res.send('Got a GET /members/:id Request');
        });
        memberRouter.post('/', function (req, res) {
          res.send('Got a POST /members Request');
        });
        memberRouter.put('/:id', function (req, res) {
          res.send('Got a PUT /members/:id Request');
        });
        memberRouter.delete('/:id', function (req, res) {
          res.send('Got a DELETE /members/:id Request');
        });
        
        export default memberRouter;
        
##### โค้ดนี้อยู่ในไฟล์ app.js

        import memberRouter from "./apps/memberRouter.js";
        
        app.use('/members', memberRouter);

## Middlewares
Middleware คือ Function ที่ถูกเรียกใช้ทำงานเวลา Server ได้รับ Request เข้ามา และจะถูก Execute ก่อน Controller Function สามารถ Input (req, res, next)
### Creating Middleware

##### โค้ดนี้อยู่ในไฟล์ assignments.validation.js
     export const validateAssignmentData = (req, res, next) => {
       const assignmentData = req.body;
       {
       <Condition Validation>
       }
        next();
      };
 
 *** req.body; คือ เอาข้อมูลใน body ไป validate

##### โค้ดนี้อยู่ในไฟล์ app.js
       import bodyParser from "body-parser";
       import fs from "fs/promises";
       import { validateAssignmentData } from "./apps/assignments.validation.js"

       const logging = (req, res, next) => {
         fs.appendFile(
           "log.txt",
           `\n IP: ${req.ip}, HTTP Method: ${req.method}, Endpoint ${req.originalUrl}`
         );
         console.log(
           `ip: ${req.ip}, Method ${req.method}, Endpoint ${req.originalUrl}`
         ); 
         next();
       };
       
       app.use(logging);
       
       app.use(bodyParser.json());
       
       app.use("/assignments", [validateAssignmentData], assignmentRouter);
