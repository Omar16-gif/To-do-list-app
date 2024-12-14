<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Advanced Todo List</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --primary-color: #4a90e2;
            --secondary-color: #f0f0f0;
            --success-color: #2ecc71;
            --danger-color: #e74c3c;
            --warning-color: #f39c12;
            --text-color: #333;
            --background-color: #f4f7f6;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background-color: var(--background-color);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            width: 100%;
            max-width: 600px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            overflow: hidden;
        }

        .header {
            background-color: var(--primary-color);
            color: white;
            padding: 20px;
            text-align: center;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header h1 {
            margin: 0;
            font-size: 1.5rem;
        }

        .input-container {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            padding: 20px;
            background-color: white;
            border-bottom: 1px solid var(--secondary-color);
        }

        #task-input {
            flex-grow: 1;
            min-width: 200px;
            padding: 10px;
            border: 2px solid var(--secondary-color);
            border-radius: 4px;
            margin-right: 10px;
            transition: border-color 0.3s ease;
        }

        .input-row {
            display: flex;
            gap: 10px;
            width: 100%;
            margin-bottom: 10px;
        }

        #deadline-input {
            flex-grow: 1;
            padding: 10px;
            border: 2px solid var(--secondary-color);
            border-radius: 4px;
        }

        .stats {
            display: flex;
            justify-content: space-between;
            padding: 10px 20px;
            background-color: var(--secondary-color);
            flex-wrap: wrap;
            gap: 10px;
        }

        .task-list-container {
            position: relative;
        }

        #task-list {
            list-style-type: none;
            max-height: 400px;
            overflow-y: auto;
        }

        .task-item {
            display: flex;
            align-items: center;
            padding: 15px 20px;
            border-bottom: 1px solid var(--secondary-color);
            transition: background-color 0.2s ease;
            position: relative;
        }

        .task-item.overdue {
            background-color: rgba(231, 76, 60, 0.1);
        }

        .task-item.due-soon {
            background-color: rgba(241, 196, 15, 0.1);
        }

        .task-checkbox {
            margin-right: 15px;
            appearance: none;
            width: 20px;
            height: 20px;
            border: 2px solid var(--primary-color);
            border-radius: 4px;
            outline: none;
            cursor: pointer;
            position: relative;
        }

        .task-checkbox:checked {
            background-color: var(--primary-color);
        }

        .task-checkbox:checked::after {
            content: '✔';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            color: white;
        }

        .task-text {
            flex-grow: 1;
            margin-right: 15px;
            transition: color 0.3s ease;
            display: flex;
            flex-direction: column;
        }

        .task-text.completed {
            text-decoration: line-through;
            color: #888;
        }

        .task-deadline {
            font-size: 0.8em;
            color: #666;
            margin-top: 5px;
        }

        .task-actions {
            display: flex;
            gap: 10px;
        }

        .deadline-chip {
            font-size: 0.7em;
            padding: 2px 5px;
            border-radius: 3px;
            margin-left: 10px;
        }

        .deadline-chip.overdue {
            background-color: var(--danger-color);
            color: white;
        }

        .deadline-chip.due-soon {
            background-color: var(--warning-color);
            color: white;
        }

        .filters {
            display: flex;
            justify-content: space-between;
            padding: 10px 20px;
            background-color: var(--secondary-color);
            flex-wrap: wrap;
            gap: 10px;
        }

        .filter-btn {
            background: none;
            border: none;
            cursor: pointer;
            padding: 5px 10px;
            border-radius: 4px;
            transition: background-color 0.3s ease;
        }

        .filter-btn.active {
            background-color: var(--primary-color);
            color: white;
        }

        .empty-state {
            text-align: center;
            padding: 50px;
            color: #888;
        }

        #priority-select, #filter-priority {
            padding: 10px;
            border: 2px solid var(--secondary-color);
            border-radius: 4px;
        }

        .add-btn {
            background-color: var(--success-color);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .add-btn:hover {
            background-color: #27ae60;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Advanced Todo List</h1>
            <div id="datetime"></div>
        </div>

        <div class="stats">
            <span>Total Tasks: <span id="total-tasks">0</span></span>
            <span>Completed: <span id="completed-tasks">0</span></span>
            <span>Overdue: <span id="overdue-tasks">0</span></span>
        </div>

        <div class="input-container">
            <div class="input-row">
                <select id="priority-select">
                    <option value="low">Low Priority</option>
                    <option value="medium" selected>Medium Priority</option>
                    <option value="high">High Priority</option>
                </select>
                <input type="text" id="task-input" placeholder="Enter a new task" maxlength="100" required>
            </div>
            <div class="input-row">
                <input 
                    type="datetime-local" 
                    id="deadline-input" 
                    min=""
                    title="Optional deadline for the task"
                >
                <button class="add-btn" onclick="todoList.addTask()">
                    <i class="fas fa-plus"></i> Add Task
                </button>
            </div>
        </div>

        <div class="filters">
            <div>
                <button class="filter-btn active" data-filter="all">All Tasks</button>
                <button class="filter-btn" data-filter="active">Active</button>
                <button class="filter-btn" data-filter="completed">Completed</button>
            </div>
            <select id="filter-priority">
                <option value="all">All Priorities</option>
                <option value="high">High Priority</option>
                <option value="medium">Medium Priority</option>
                <option value="low">Low Priority</option>
            </select>
        </div>

        <div class="task-list-container">
            <ul id="task-list"></ul>
        </div>
    </div>

    <script>
        class TodoList {
            constructor() {
                // Set minimum deadline to current time
                const now = new Date();
                document.getElementById('deadline-input').min = 
                    now.toISOString().slice(0, 16);

                this.tasks = JSON.parse(localStorage.getItem('tasks') || '[]');
                
                // Convert stored date strings back to Date objects
                this.tasks.forEach(task => {
                    if (task.deadline) {
                        task.deadline = new Date(task.deadline);
                    }
                });

                this.currentFilter = 'all';
                this.currentPriorityFilter = 'all';
                
                this.initEventListeners();
                this.updateDateTime();
                this.render();
                
                // Update date, time, and task status every minute
                this.statusCheckInterval = setInterval(() => {
                    this.updateDateTime();
                    this.render();
                }, 60000);
            }

            updateDateTime() {
                const now = new Date();
                const dateTimeElement = document.getElementById('datetime');
                dateTimeElement.innerHTML = `
                    ${now.toLocaleDateString()} 
                    <small>${now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}</small>
                `;
            }

            initEventListeners() {
                // Filter buttons
                document.querySelectorAll('.filter-btn').forEach(btn => {
                    btn.addEventListener('click', (e) => {
                        document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
                        e.target.classList.add('active');
                        this.currentFilter = e.target.dataset.filter;
                        this.render();
                    });
                });

                // Priority filter
                document.getElementById('filter-priority').addEventListener('change', (e) => {
                    this.currentPriorityFilter = e.target.value;
                    this.render();
                });

                // Input field event listeners
                const taskInput = document.getElementById('task-input');

                // Add task on Enter key
                taskInput.addEventListener('keypress', (e) => {
                    if (e.key === 'Enter' && taskInput.value.trim() !== '') {
                        this.addTask();
                    }
                });
            }

            addTask() {
                const input = document.getElementById('task-input');
                const prioritySelect = document.getElementById('priority-select');
                const deadlineInput = document.getElementById('deadline-input');
                const taskText = input.value.trim();
                
                if (taskText && taskText.length > 0 && taskText.length <= 100) {
                    const task = {
                        id: Date.now(),
                        text: taskText,
                        completed: false,
                        priority: prioritySelect.value,
                        createdAt: new Date(),
                        deadline: deadlineInput.value ? new Date(deadlineInput.value) : null
                    };
                    
                    this.tasks.push(task);
                    this.saveAndRender();
                    
                    // Reset inputs
                    input.value = '';
                    deadlineInput.value = '';
                } else {
                    alert('Please enter a valid task (1-100 characters)');
                }
            }

            calculateTaskStatus(task) {
                if (task.completed) return 'completed';
                
                if (task.deadline) {
                    const now = new Date();
                    const deadline = new Date(task.deadline);
                    
                    // Due soon if within next 24 hours
                    const oneDayFromNow = new Date(now.getTime() + 24 * 60 * 60 * 1000);
                    
                    if (deadline < now) return 'overdue';
                    if (deadline <= oneDayFromNow) return 'due-soon';
                }
                
                return 'active';
            }

            formatDeadline(deadline) {
                if (!deadline) return '';
                
                const now = new Date();
                const deadlineDate = new Date(deadline);
                
                // If deadline is today, show time
                if (deadlineDate.toDateString() === now.toDateString()) {
                    return `Today at ${deadlineDate.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'})}`;
                }
                
                // Otherwise, show date and time
                return deadlineDate.toLocaleString();
            }

            toggleComplete(taskId) {
                const task = this.tasks.find(t => t.id === taskId);
                if (task) {
                    task.completed = !task.completed;
                    this.saveAndRender();
                }
            }

            editTask(taskId) {
                const task = this.tasks.find(t => t.id === taskId);
                if (task) {
                    const newText = prompt('Edit task:', task.text);
                    if (newText !== null && newText.trim() !== '' && newText.trim().length <= 100) {
                        task.text = newText.trim();
                        this.saveAndRender();
                    } else if (newText !== null) {
                        alert('Please enter a valid task (1-100 characters)');
                    }
                }
            }

            deleteTask(taskId) {
                this.tasks = this.tasks.filter(task => task.id !== taskId);
                this.saveAndRender();
            }

            saveAndRender() {
                localStorage.setItem('tasks', JSON.stringify(this.tasks));
                this.render();
            }

            render() {
                const list = document.getElementById('task-list');
                const totalTasksElement = document.getElementById('total-tasks');
                const completedTasksElement = document.getElementById('completed-tasks');
                const overdueTasksElement = document.getElementById('overdue-tasks');

                list.innerHTML = '';

                // Apply filters
                let filteredTasks = this.tasks.filter(task => {
                    // Status filter
                    const statusFilter = 
                        this.currentFilter === 'active' ? !task.completed :
                        this.currentFilter === 'completed' ? task.completed : 
                        true;

                    // Priority filter
                    const priorityFilter = 
                        this.currentPriorityFilter === 'all' || 
                        task.priority === this.currentPriorityFilter;

                    return statusFilter && priorityFilter;
                });

                // Sort tasks
                filteredTasks.sort((a, b) => {
                    const priorityOrder = { 'high': 3, 'medium': 2, 'low': 1 };
                    
                    // First by priority
                    if (priorityOrder[b.priority] !== priorityOrder[a.priority]) {
                        return
