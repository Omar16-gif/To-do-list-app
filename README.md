<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
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

        #prio
