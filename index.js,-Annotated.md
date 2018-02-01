```javascript
// WebSocket connection setup
var socket = io();
var questionRecieved=false;
var output = document.getElementById('output');	
output.innerHTML = "<h1 id=response </h1>";
```
**_variable declaration_**  of the objects that need to be addressed frqeuntly or that need to be kept track of during one session.
1. with ```socket = io();``` we create a socket client that will connect back to the node.js server running `ChatServer.js`
1. ```questionRecieved``` keeps track of whether or not we have recieved a question, to avoid sending empty or unwanted messages
1. The ```output``` object is the response field from the ChatBot that needs to be freqeuntly changed 

```javascript
function sendMessage() {
    var input = document.getElementById("input").value;
    socket.emit('message',input);
    document.getElementById("input").value="";
    document.getElementById("input").style.display="none";
}
```
This function is called to send answers to the server.
1. reads the written message
1. sends it over the socket connection to the server with ```socket.emit(...)```
1. empties the text field and...
1. ... finally turns the field invisible with ```.style.display="none"```


```javascript
$(document).keypress(function(e) {
  if (e.which == 13 && questionRecieved===true) {
    questionRecieved=false;
    sendMessage();// run bot function when enter key pressed
  }
});
```
This function is called when an 'return-key' press is detected.

```javascript
function changeText(input){
document.getElementById('response').textContent = input;
}
```
This function is called whenever the response from the ChatBot on the webpage needs to be changed. It finds the correct object with the 'response' ID and changes the ```.textContent```

```javascript
socket.on('answer', function(msg) {
  console.log('Incomming answer:', msg);
  changeText(msg);
});
socket.on('question', function(msg) {
  console.log('Incomming Question:', msg);
  questionRecieved=true;
  document.getElementById("input").style.display="block";
  changeText(msg);
});
socket.on('changeBG', function(msg) {
  console.log('Changeing backgroundColor to:', msg);
  document.body.style.backgroundColor = msg;
});
socket.on('changeFont', function(msg) {
  console.log('Changeing Font to:', msg);
  var h1 = document.getElementById('response');
  h1.style.color = 'white';
});
```
These four functions correspond to strict messages that the server can send to the client. The first element of this function is the type of message (e.g. ```changeFont```) and the second part is the function to execute when such a message is recieved e.g. ```function(msg) {  console.log('Changeing Font to:', msg); ...```


```javascript
socket.on('connect',function(){
  socket.emit('loaded');
});
```
This function is similar to the above. It is a workaround function to make sure that the server-client connection is running and stable before the server starts sending messages. 