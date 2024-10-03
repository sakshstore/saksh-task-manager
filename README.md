# Saksh Task Manager

## Description

**Saksh Task Manager** is a Node.js module designed for efficient task management, featuring caching and event handling capabilities. It utilizes **NodeCache** for caching and **EventEmitter** for managing task-related events. Each task is associated with a user ID, making it suitable for multi-user environments.

## Installation

To install the module, run the following command:

```bash
npm install saksh-task-manager
```

## Usage

### Importing the Module

To use the Saksh Task Manager, import the module as follows:

```javascript
const SakshTaskController = require('saksh-task-manager');
```

### Creating an Instance

When creating an instance of `SakshTaskController`, you need to provide a user ID:

```javascript
const userId = 'your-user-id-here';
const taskController = new SakshTaskController(userId);
```

## Methods

### `sakshGetTasks()`

Retrieves all tasks for the user with caching.

**Returns:**
- An array of tasks.

### `sakshCreateTask(taskData)`

Creates a new task for the user.

**Parameters:**
- `taskData` (Object): The data for the task.

**Returns:**
- The created task.

### `sakshUpdateTask(id, taskData)`

Updates an existing task for the user.

**Parameters:**
- `id` (String): The task ID.
- `taskData` (Object): The updated task data.

**Returns:**
- The updated task.

### `sakshDeleteTask(id)`

Deletes a task for the user.

**Parameters:**
- `id` (String): The task ID.

**Returns:**
- A message indicating that the task was deleted.

## Event Handling

The module employs an **EventEmitter** to handle task-related events. The following events are emitted:

- `taskCreated`: Emitted when a new task is created.
- `taskUpdated`: Emitted when a task is updated.
- `taskDeleted`: Emitted when a task is deleted.
- `tasksRetrieved`: Emitted when tasks are retrieved.

## Example

Here’s a simple example demonstrating how to use the Saksh Task Manager:

```javascript
const SakshTaskController = require('saksh-task-manager');
const mongoose = require('mongoose');

const run = async () => {
    try {
        // Connect to MongoDB
        await mongoose.connect('mongodb://localhost:27017/sakshtask', {
            useNewUrlParser: true,
            useUnifiedTopology: true,
        });
        console.log('MongoDB connected');

        // Create an instance of SakshTaskController with a user ID
        const userId = 'your-user-id-here';  // this can be user email id also
        const taskController = new SakshTaskController(userId);

        // Create a new task
        const newTask = await taskController.sakshCreateTask({ name: 'Sample Task', fileUrl: 'http://example.com/file.pdf' });
        console.log('Task Created:', newTask);

        // Get all tasks
        const tasks = await taskController.sakshGetTasks();
        console.log('All Tasks:', tasks);

        // Update a task
        const updatedTask = await taskController.sakshUpdateTask(newTask._id, { completed: true });
        console.log('Task Updated:', updatedTask);

        // Delete a task
        const deleteMessage = await taskController.sakshDeleteTask(newTask._id);
        console.log(deleteMessage);

    } catch (error) {
        console.error('Error:', error.message);
    }
};

run();
```

## Contributing

If you would like to contribute, please fork the repository and use a feature branch. Pull requests are warmly welcome!

## License

This project is licensed under the **MIT License** - see the LICENSE file for details.

## Contact

If you have any questions or suggestions, feel free to reach out to **susheelhbti**.
