# Expense Tracker (ReactJS)
## Date:24/05/2025

## AIM
To develop a simple Expense Tracker application using React that allows users to manage their personal finances by adding, viewing, and deleting income and expense transactions, while dynamically calculating the current balance, total income, and total expenses.

## ALGORITHM
### STEP 1: Initialize the Project
Create a new React app using:

npx create-react-app expense-tracker
or

npm create vite@latest expense-tracker --template react

Open the project in a code editor like VS Code.

### Step 2: Setup State
Define a state variable to store transactions:

Example: const [transactions, setTransactions] = useState([])

Define state variables for the form inputs:

const [text, setText] = useState("")

const [amount, setAmount] = useState("")

### Step 3: Add a New Transaction
Create a form with two inputs:

Text input for description

Number input for amount

On form submit:

Validate input

Create a new transaction object

Add the object to the transactions array using setTransactions.

### Step 4: Display Transaction List

Use map() to render each transaction in a list.

Conditionally style each item based on amount > 0 (income) or amount < 0 (expense).

Add a delete button next to each transaction.

### Step 5: Calculate and Display Summary

Use reduce() to calculate:

Total Balance: sum of all amounts

Total Income: sum of all positive amounts

Total Expenses: sum of all negative amounts

Display these values at the top of the UI.

### Step 6: Delete a Transaction

When delete is clicked:

Use filter() to remove the transaction from the array by id.

Update the state using setTransactions.

### Step 7: Style the Application

Use basic CSS to style:

Balance summary

Income/expense totals

Form inputs

Transaction list (with color coding)

## PROGRAM
app.js
```
import React, { useState } from 'react';
import './App.css';

function App() {
  const [transactions, setTransactions] = useState([]);
  const [text, setText] = useState('');
  const [amount, setAmount] = useState('');

  const handleAddTransaction = (e) => {
    e.preventDefault();
    if (!text || isNaN(amount) || amount === '') return;

    const newTransaction = {
      id: Date.now(),
      text,
      amount: parseFloat(amount),
    };

    setTransactions([newTransaction, ...transactions]);
    setText('');
    setAmount('');
  };

  const handleDeleteTransaction = (id) => {
    setTransactions(transactions.filter(txn => txn.id !== id));
  };

  const balance = transactions.reduce((acc, txn) => acc + txn.amount, 0);
  const income = transactions.filter(txn => txn.amount > 0).reduce((acc, txn) => acc + txn.amount, 0);
  const expense = transactions.filter(txn => txn.amount < 0).reduce((acc, txn) => acc + txn.amount, 0);

  return (
    <div className="container">
      <h2>💰 Expense Tracker</h2>

      <div className="summary">
        <h3>Balance: ₹{balance.toFixed(2)}</h3>
        <div className="totals">
          <div className="income">Income: ₹{income.toFixed(2)}</div>
          <div className="expense">Expense: ₹{Math.abs(expense).toFixed(2)}</div>
        </div>
      </div>

      <form onSubmit={handleAddTransaction} className="transaction-form">
        <input
          type="text"
          placeholder="Description (e.g. Salary, Food)"
          value={text}
          onChange={(e) => setText(e.target.value)}
        />
        <input
          type="number"
          placeholder="Amount (e.g. 500, -200)"
          value={amount}
          onChange={(e) => setAmount(e.target.value)}
        />
        <button type="submit">Add Transaction</button>
      </form>

      <ul className="transaction-list">
        {transactions.map(txn => (
          <li key={txn.id} className={txn.amount > 0 ? 'plus' : 'minus'}>
            <span>{txn.text}</span>
            <span>₹{txn.amount.toFixed(2)}</span>
            <button onClick={() => handleDeleteTransaction(txn.id)}>x</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;

```
app.css
```
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 400px;
  margin: 40px auto;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

h2, h3 {
  text-align: center;
}

.summary {
  margin-bottom: 20px;
}

.totals {
  display: flex;
  justify-content: space-around;
  margin-top: 10px;
}

.income {
  color: green;
}

.expense {
  color: red;
}

.transaction-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.transaction-form input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.transaction-form button {
  padding: 8px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.transaction-form button:hover {
  background-color: #0056b3;
}

.transaction-list {
  list-style: none;
  padding: 0;
  margin-top: 20px;
}

.transaction-list li {
  display: flex;
  justify-content: space-between;
  padding: 8px;
  margin: 6px 0;
  border-radius: 4px;
}

.transaction-list li.plus {
  background-color: #d4edda;
  color: green;
}

.transaction-list li.minus {
  background-color: #f8d7da;
  color: red;
}

.transaction-list button {
  background: transparent;
  border: none;
  color: #333;
  font-size: 16px;
  cursor: pointer;
}

```

## OUTPUT

![Screenshot 2025-05-24 103355](https://github.com/user-attachments/assets/5af34fd7-c7cb-4324-b8d9-ea45edd1b67c)

## RESULT
A fully functional React-based Expense Tracker application was successfully developed. 
