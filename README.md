# NodeJS
Node.js is a JavaScript runtime environment that runs on the V8 engine. It executes JavaScript code outside a web browser.
  
We can execute a JavaScript file using Node.js with the CLI command node <js_file_path>.

## File System
fs Module: fs stand for "File System" is module in Node.js and use manage file in computer.

    reading file => fs.readFile("fillepath", function)

    Write file (OverWrite) => fs.writeFile("fillepath", function)

    Write append data onto existing file => fs.appendFile("fillepath", function)

    Delete file => unlinkFile("fillepath", function)

    In Node.js, we use .catch to handle errors in promises.

    In Node.js, we use try ... catch to handle errors with the await keyword.

## API
  ##### HTTP Request Method 
    GET => for Created
    
    POST => for Add
    
    PUT => for Updated
    
    DELETE => for Deleted
    
  ##### Creating API Routes.
  - `app.method(path, handler)`
    - `app` คือ Express Object
    - `method` คือ HTTP Request Method เช่น `get`, `post`, `put`, `delete`
    - `path` คือ API Endpoint บน Server เช่น `/posts`
        - `path` สามารถกำหนดเป็น Parameter ได้ เช่น `/posts/:postId` ซึ่ง `:postId` คือ Parameter
    - `handler` คือ Controller ที่จะทำงานเมื่อ Request วิ่งเข้ามาตาม Route ที่กำหนด
  ##### Returning Responses.
  -`ใน Express เราสามารถสร้าง Response ได้ด้วย Object res.send()`
  
  -`Express สามารถส่ง Response กลับเป็น JSON ได้ด้วย res.json() ซึ่งรับ Input เป็น JavaScript Objec`
  

## Express
Start: npm install express






## Router




## Middlewares

