```javascript
var express = require('express'); // web server application
var app = express(); // webapp
var http = require('http').Server(app); // connects http library to server
var io = require('socket.io')(http); // connect websocket library to server
var serverPort = 8000;
```
**_Variable declaration._** 
Note:
* the invocation of 'express', which is a server application 
* the attachment of the http library, which makes it a webserver 
* the attachment of the WebSocket library(```socket.io```), which acts as a real-time communication link between the server and client


```javascript
app.use(express.static('public')); // find pages in public directory

// start the server and say what port it is on
http.listen(serverPort, function() {
  console.log('listening on *:%s', serverPort);
});
```
**_Starting the ChatBot Server_**
Starting the webserver telling it to server files found in folder ```'public'```

```javascript
// this is the websocket event handler and say if someone connects
// as long as someone is connected, listen for messages
io.on('connect', function(socket) {
  console.log('a new user connected');
  var questionNum = 0; // keep count of question, used for IF condition.
  socket.on('loaded', function(){ // we wait until the client has loaded and contacted us that it is ready to go.

    socket.emit('answer', "Hey, hello I am \"___*-\" a simple chat bot example."); // We start with the introduction;
    setTimeout(timedQuestion, 5000, socket, "What is your name?"); // Wait a moment and respond with a question.

  });
  socket.on('message', (data) => { // If we get a new message from the client we process it;
    console.log(data);
    questionNum = bot(data, socket, questionNum); // run the bot function with the new message
  });
  socket.on('disconnect', function() { // This function  gets called when the browser window gets closed
    console.log('user disconnected');
  });
});
```
**_Client connection._** 
This specifies what to do with connections and messages from clients (e.g. you on the web browser!). This section initializes the ChatBot, waits for the load message from the [client](index.js,-annotated) and handles the incoming and outgoing traffic.


```javascript
function bot(data,socket,questionNum) {
  var input = data; // This is generally really terrible from a security point of view ToDo avoid code injection
  var answer;
  var question;
  var waitTime;

/// These are the main statements that make up the conversation.
  if (questionNum == 0) {
    answer= 'Hello ' + input + ' :-)';// output response
    waitTime = 5000;
    question = 'How old are you?';			    
  } else if (questionNum == 1) {
    answer= 'Really, ' + input + ' years old? So that means you were born in: ' + (2018-parseInt(input)); // output response
    waitTime = 5000;
    question = 'Where do you live?';	
  } else if (questionNum == 2) {
    answer = 'Cool! I have never been to ' + input+'.';
    waitTime = 5000;
    question = 'Whats your favorite color?';
  } else if (questionNum == 3) {
    answer = 'Ok, ' + input+' it is.';
    socket.emit('changeBG', input.toLowerCase());
    waitTime = 5000;
    question = 'Can you still read the font?';
  } else if (questionNum == 4) {
    if (input.toLowerCase() === 'yes' || input === 1){
      answer = 'Perfect!';
      waitTime = 5000;
      question = 'Whats your favorite place?';
    } else if (input.toLowerCase() === 'no' || input === 0){
      socket.emit('changeFont','white'); // We really should look up the inverse of what we said before.
      answer = 'How about now?'
      question = '';
      waitTime = 0;
      questionNum--; // Here we go back in the question number this can end up in a loop!
    } else {
      question = 'Can you still read the font?'; // load next question
      answer = 'I did not understand you. Could you please answer "yes" or "no"?'
      questionNum--;
      waitTime = 5000;
    }
  // load next question
  } else {
    answer= 'I have nothing more to say!';// output response
    waitTime = 0;
    question = '';
  }


  /// We take the changed data and distribute it to the required objects.
  socket.emit('answer',answer);
  setTimeout(timedQuestion, waitTime,socket,question);
  return (questionNum+1);
}
```
**_ChatBot 'decision tree'_**
These are the answers and questions the chatbot will say. The long if and else statement can be easily modified to change the responses.
**Note:**
* ```questionNum``` keeps track of where we are in the conversation tree. 
* ```waitTime``` Sets how long in milliseconds the ```answer``` is shown before the server sends the next question. 
* ```answer``` The 'answer' type message does not enable the input field.
* ```question``` poses a question to the user and enables the input field.

```javascript
function timedQuestion(socket,question) {
  if(question!=''){
    socket.emit('question',question);
  } else {
    //console.log('No Question send!');
  }
}
```
**_waiting function_**
Once the time, as set in ```waitTime```, has run out the question is send to the client if the question is not empty.
