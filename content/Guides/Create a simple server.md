
Sometimes, there could be a need to create or test a side-project, and it turns out it cannot be run in browser environment. There could be pletny of reasons for that - for example because of CORS policy, or the code might be fetching data, which for security reasons, cannot be used inside a browser. Here is when a web server saves the day!

<br>

## S1. Create root directory

First off all, create a directory which will be the project root. It will further contain a server file and HTML template, CSS stylesheet and JS script file.

Open Command Prompt (CMD) and write the following command:

```
📁 mkdir  myProject  
```

Above will create a new folder in current directory.

Now go to the newly created folder by using this CMD command:

```
➡️ cd  myProject
```

<br>

## S2. Create project files

Next up, we need to **structure our project** by adding a few important files and directories. Taking a minimalistic approach, here is the example structure of a custom server:

```
 📁 myProject
 |
 |----🗒️server.js
 |
 |----📁 public 
       |
       |---- 🗒️ index.html
       |
       |---- 🗒️ style.css
       |
       |---- 🗒️ script.js

```

<br>

## S3. Install Express.js

To simplify the creation process of a server, we will make use of Express.js, which is a popular, lightweight JavaScript web framework to create web applications. Now, inside the newly created folder, install Express.js :

```
▶️ npm install express --save
```

<br>

##  S4. Create server inside server.js

The essential step will be to add a logic that creates an accessible server that may handle some files. Here is how to achieve it:

### server.js

```
const express = require('express')
const app = express()
const port = 3000;

app.use(express.static('public'))

app.listen(port, () => {
    console.log(`Example app listening on: http://localhost:${port}`);
})
```

<br> 

##  S5. Add code to remain files

Now it is time to include some meaningful code inside newly created files. Below you can find some example content of each file, that will follow project structure defined in `S2`.

### index.html

```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title> A simple server </title>
		<link rel="stylesheet" href="./style.css" />
	</head>

	<body>
        <div class="title"> Test content </div>  

        <script src="script.js"></script>
	</body>
</html>
```

### style.css

```
html {
    font-size: 12px;
}

*, *::before, *::after {
    box-sizing: border-box;
    margin: 0 auto;
    border: 2px solid #444;
}

body {
    font-family: 'Arial', sans-serif;
    background: #222;
    color: #ddd;
    min-height: 100vh;
    width: 100%;
}

.title {
    font-size: 2rem;
    text-align: center;
}
```

### script.js

```
console.log('Hello world!');
```

<br>

## S6. Run the server

Now when everything is set up properly, it is the high time to invoke the server and test if everything works as expected.

Being inside the root directory,  in Command Prompt (CMD) use a Node command to run a server script file (here provide your actual server file name in case it is not named *server.js*) :

```
▶️ node  server.js 
```

To make above command even more convenient to write, the `.js` extension can be omitted, which will make the command work the same way:

```
▶️ node  server
```
