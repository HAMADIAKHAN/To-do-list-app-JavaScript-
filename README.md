# To-do-list-app-JavaScript-
This project showcases my skills in:  - Front-end development using HTML, CSS, and JavaScript - Creating a functional task manager with features like task addition, deletion, editing, and completion - Implementing local storage to save tasks  This project was a great opportunity to practice my coding skills and learn new techniques. 

// Get the task list and input field elements
const taskList = document.getElementById('task-list');
const newTaskInput = document.getElementById('new-task');

// Add event listeners to task list items
taskList.addEventListener('click', (event) => {
  if (event.target.tagName === 'LI') {
    // Task deletion
    if (event.target.classList.contains('delete')) {
      event.target.remove();
    }
    // Task editing
    else if (event.target.classList.contains('edit')) {
      const taskText = event.target.textContent;
      const editInput = document.createElement('input');
      editInput.value = taskText;
      event.target.replaceWith(editInput);
      editInput.focus();
      editInput.addEventListener('blur', () => {
        const newTaskText = editInput.value.trim();
        const newTaskListItem = document.createElement('li');
        newTaskListItem.textContent = newTaskText;
        taskList.replaceChild(newTaskListItem, editInput);
      });
    }
    // Task completion (checkbox)
    else {
      event.target.classList.toggle('completed');
    }
  }
});

// Add an event listener to the "Add Task" button
document.getElementById('add-task').addEventListener('click', addTask);

// Function to add a new task
function addTask() {
  // Get the new task text
  const newTaskText = newTaskInput.value.trim();
  
  // Create a new list item
  const listItem = document.createElement('li');
  listItem.textContent = newTaskText;
  
  // Add a delete button
  const deleteButton = document.createElement('button');
  deleteButton.textContent = 'Delete';
  deleteButton.classList.add('delete');
  listItem.appendChild(deleteButton);
  
  // Add an edit button
  const editButton = document.createElement('button');
  editButton.textContent = 'Edit';
  editButton.classList.add('edit');
  listItem.appendChild(editButton);
  
  // Add a checkbox
  const checkbox = document.createElement('input');
  checkbox.type = 'checkbox';
  listItem.appendChild(checkbox);
  
  // Add the list item to the task list
  taskList.appendChild(listItem);
  
  // Clear the input field
  newTaskInput.value = '';
}
