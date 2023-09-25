<!DOCTYPE html>
<html>
<head>
  <title>Content Management Tool</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
    }

    h1 {
      margin-bottom: 20px;
    }

    form {
      margin-bottom: 20px;
    }

    label {
      display: block;
      margin-bottom: 10px;
    }

    textarea, input[type="text"] {
      width: 100%;
      padding: 5px;
      margin-bottom: 10px;
    }

    input[type="submit"] {
      padding: 10px 20px;
      background-color: #337ab7;
      color: #fff;
      border: none;
      cursor: pointer;
    }

    #detailsContainer {
      margin-top: 30px;
    }

    #detailsContainer h1 {
      font-size: 24px;
      margin-bottom: 10px;
    }

    #detailsContainer h2 {
      font-size: 18px;
      margin-bottom: 5px;
    }

    #detailsContainer p {
      margin-bottom: 10px;
    }

    #detailsContainer img {
      max-width: 100%;
      margin-bottom: 10px;
    }
  </style>
  <script>
    // Access the form and register the form submission event
    document.addEventListener('DOMContentLoaded', function() {
      var form = document.querySelector('#blogForm');
      form.addEventListener('submit', function(event) {
        event.preventDefault(); // Prevent the form from submitting

        // Retrieve the form values
        var title = document.querySelector('#title').value;
        var content = document.querySelector('#content').value;
        var image = document.querySelector('#image').value;
        var video = document.querySelector('#video').value;

        // Display the filled details on the webpage
        var detailsContainer = document.querySelector('#detailsContainer');
        detailsContainer.innerHTML = `
          <h1>Blog Details</h1>
          <h2>Title: ${title}</h2>
          <p>Content: ${content}</p>
          <img src="${image}" alt="Blog Image">
          <p>Video URL: ${video}</p>
        `;
      });
    });
  </script>
</head>
<body>
  <h1>Content Management Tool</h1>
  <form id="blogForm">
    <label for="title">Title:</label>
    <input type="text" id="title" name="title">

    <label for="content">Content:</label>
    <textarea id="content" name="content" rows="4"></textarea>

    <label for="image">Image:</label>
    <input type="text" id="image" name="image">

    <label for="video">Video URL:</label>
    <input type="text" id="video" name="video">

    <input type="submit" value="Create Blog">
  </form>

  <div id="detailsContainer"></div>
</body>
</html>


app.js


// Sample data for tasks, users, and messages
let tasks = [];
let users = [];
let messages = [];

// Task form and list elements
const taskForm = document.getElementById('task-form');
const taskInput = document.getElementById('task-input');
const assigneeSelect = document.getElementById('assignee-select');
const taskList = document.getElementById('task-list');

// User form and list elements
const userForm = document.getElementById('user-form');
const userInput = document.getElementById('user-input');
const userList = document.getElementById('user-list');

// Chat form and list elements
const messageForm = document.getElementById('message-form');
const messageInput = document.getElementById('message-input');
const messageList = document.getElementById('message-list');

// Function to render tasks
function renderTasks() {
  taskList.innerHTML = '';
  tasks.forEach(task => {
    const li = document.createElement('li');
    li.textContent = task;
    taskList.appendChild(li);
  });
}

// Function to render users
function renderUsers() {
  userList.innerHTML = '';
  assigneeSelect.innerHTML = '<option value="">Assignee</option>';
  users.forEach(user => {
    const li = document.createElement('li');
    li.textContent = user;
    userList.appendChild(li);

    // Add user as an option in assignee select
    const option = document.createElement('option');
    option.value = user;
    option.textContent = user;
    assigneeSelect.appendChild(option);
  });
}

// Function to render chat messages
function renderMessages() {
  messageList.innerHTML = '';
  messages.forEach(message => {
    const li = document.createElement('li');
    li.textContent = message;
    messageList.appendChild(li);
  });
}

// Event listener for task form submission
taskForm.addEventListener('submit', e => {
  e.preventDefault();
  const task = taskInput.value.trim();
  const assignee = assigneeSelect.value;
  if (task !== '' && assignee !== '') {
    tasks.push(`${task} (Assigned to: ${assignee})`);
    renderTasks();
    taskInput.value = '';
    assigneeSelect.value = '';
  }
});

// Event listener for user form submission
userForm.addEventListener('submit', e => {
  e.preventDefault();
  const user = userInput.value.trim();
  if (user !== '') {
    users.push(user);
    renderUsers();
    userInput.value = '';
  }
});

// Event listener for message form submission
messageForm.addEventListener('submit', e => {
  e.preventDefault();
  const message = messageInput.value.trim();
  if (message !== '') {
    messages.push(message);
    renderMessages();
    messageInput.value = '';
  }
});

// Initial rendering of tasks, users, and messages
renderTasks();
renderUsers();
renderMessages();
