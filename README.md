const readline = require('readline');

// Setup readline interface
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

// In-memory array to store tasks
let tasks = [];

// Function to show menu
function showMenu() {
    console.log('\n--- TASK MANAGER ---');
    console.log('1. View all tasks');
    console.log('2. Add a new task');
    console.log('3. Update a task');
    console.log('4. Delete a task');
    console.log('5. Exit');

    rl.question('Choose an option: ', (choice) => {
        handleChoice(choice);
    });
}

// Handle user input
function handleChoice(choice) {
    switch(choice) {
        case '1':
            viewTasks();
            break;
        case '2':
            addTask();
            break;
        case '3':
            updateTask();
            break;
        case '4':
            deleteTask();
            break;
        case '5':
            console.log('Exiting...');
            rl.close();
            break;
        default:
            console.log('Invalid choice. Try again.');
            showMenu();
    }
}

// View all tasks
function viewTasks() {
    console.log('\n--- ALL TASKS ---');
    if(tasks.length === 0) {
        console.log('No tasks available.');
    } else {
        tasks.forEach((task, index) => {
            console.log(`${index + 1}. ${task}`);
        });
    }
    showMenu();
}

// Add a new task
function addTask() {
    rl.question('Enter task description: ', (desc) => {
        tasks.push(desc);
        console.log('Task added successfully!');
        showMenu();
    });
}

// Update a task
function updateTask() {
    rl.question('Enter task number to update: ', (num) => {
        const index = parseInt(num) - 1;
        if(index >= 0 && index < tasks.length) {
            rl.question('Enter new description: ', (desc) => {
                tasks[index] = desc;
                console.log('Task updated!');
                showMenu();
            });
        } else {
            console.log('Invalid task number.');
            showMenu();
        }
    });
}

// Delete a task
function deleteTask() {
    rl.question('Enter task number to delete: ', (num) => {
        const index = parseInt(num) - 1;
        if(index >= 0 && index < tasks.length) {
            tasks.splice(index, 1);
            console.log('Task deleted!');
        } else {
            console.log('Invalid task number.');
        }
        showMenu();
    });
}

// Start the application
showMenu();
