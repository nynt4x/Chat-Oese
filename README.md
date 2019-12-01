# Chat-Oese
Chat application using Nodejs & SocketIO
1. Make sure Node.JS is installed, we will be using NPM a couple of times during our development.
- NPM stands for Node Package Manager
and is used to install packages and dependencies that apps might need to run.

2. After installing NodeJS we need to create a package.json file. 
- Within this file we will be creating some information about our app and what packages will be needed to run it. 
{
  "name": "socket-chat-example",
  "version": "0.0.1",
  "description": "my first socket.io app",
  "dependencies": {}
}
- To fill our dependencies simply install the packages you need within your project directory using the terminal. 
"npm install express@4.15.2"

3. Now that express is installed we want to create our index.js file.
var app = require('express')();
var http = require('http').createServer(app);

app.get('/', function(req, res){
  res.send('<h1>Hello world</h1>');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});

- Express initializes app to be a function handler that you can supply to an HTTP server (as seen in line 2).
- We define a route handler / that gets called when we hit our website home.
- We make the http server listen on port 3000.
- Try to write "node index.js" in your terminal
- Go to http://localhost:3000 in your browser

4. After we've tested the server we want to make it serve our HTML file instead of a hello world example. 
- First we go into our index.js file and re-adjust our app.get line to send a file instead of a HTML string. 

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

- Now that we've adjusted our line to serve a HTML site instead of a HTML string, we will create a index.html file inside the project folder.
- Here we will paste the Chat Template which we've been working on for some time now. 


5. For the next part we need to install another package using "npm install socket.io", socket.io is a package which provides live syncronization, a must have for any chat application. 
- Now we will go back into our index.js to integrate socket.io

var app = require('express')();
var http = require('http').createServer(app);
var io = require('socket.io')(http);

app.get('/', function(req, res){
  res.sendFile(__dirname + '/index.html');
});

io.on('connection', function(socket){
  console.log('a user connected');
});

http.listen(3000, function(){
  console.log('listening on *:3000');
});

- We initialize socket.io and pass is the http server object. Then we create a function whichs listens and console logs incoming events to the console. 
- Then we go into our index.html for the last part of the integration, add the following script before closing your </body> tag.

<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io();
</script>

- Now try to run your code again using "node index.js" in your terminal, if are listening on http://localhost:3000/ and if you open the browser your console tells you that "a user connected". 
- Now we can go into our index.js and add a disconnect log, so we can see when our users leave the site again.

io.on('connection', function(socket){
  console.log('a user connected');
  socket.on('disconnect', function(){
    console.log('user disconnected');
  });
});

- Now if we run our project again using "node index.js" and open a couple of browsers, you can see that users are connecting in the console and if you close them you can see that users are disconnecting in the console. 

6.


