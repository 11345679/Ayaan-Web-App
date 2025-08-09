# Ayaan-Web-App
<!DOCTYPE html>
<html>
<head>
<title>AYAAN EXPENSE CALCULATOR</title>
<style>
    body {
        font-family: Arial, sans-serif;
        text-align: center;
        margin: 0;
        background-color: #f2f2f2;
        background-size: cover;
        min-height: 100vh;
        position: relative;
    }
    h1 {
        font-size: 30px;
        margin-top: 20px;
    }
    .background-text {
        position: fixed;
        top: 50%;
        left: 50%;
        font-size: 50px;
        color: rgba(0,0,0,0.1);
        transform: translate(-50%, -50%);
        white-space: nowrap;
        pointer-events: none;
        z-index: 0;
    }
    .container {
        position: relative;
        z-index: 1;
    }
    input, select, button {
        padding: 10px;
        margin: 5px;
        border-radius: 5px;
        border: 1px solid #ccc;
    }
    .expenses {
        margin-top: 20px;
        text-align: left;
        display: inline-block;
        background: white;
        padding: 10px;
        border-radius: 5px;
    }
</style>
</head>
<body>
<div class="background-text">AYAAN EXPENSE CALCULATOR</div>
<div class="container">
    <h1>AYAAN EXPENSE CALCULATOR</h1>
    <input type="number" id="amount" placeholder="Amount">
    <input type="text" id="description" placeholder="Description">
    <input type="date" id="date">
    <select id="dateType">
        <option value="auto">Auto Date</option>
        <option value="custom">Custom Date</option>
    </select>
    <br>
    <button onclick="addExpense()">Add Expense</button>
    <input type="color" id="bgColor" onchange="changeBackground()">

    <div class="expenses" id="expenseList">
        <h3>Expenses</h3>
        <ul id="list"></ul>
    </div>
</div>

<script>
    let expenses = JSON.parse(localStorage.getItem("expenses")) || [];

    function addExpense() {
        let amount = document.getElementById("amount").value;
        let description = document.getElementById("description").value;
        let dateType = document.getElementById("dateType").value;
        let date = (dateType === "auto") ? new Date().toISOString().split('T')[0] : document.getElementById("date").value;

        if(amount && description) {
            expenses.push({amount, description, date});
            localStorage.setItem("expenses", JSON.stringify(expenses));
            displayExpenses();
        }
    }

    function displayExpenses() {
        let list = document.getElementById("list");
        list.innerHTML = "";
        expenses.forEach((exp, index) => {
            let li = document.createElement("li");
            li.innerHTML = `${exp.date} - ₹${exp.amount} - ${exp.description}`;
            list.appendChild(li);
        });
    }

    function changeBackground() {
        document.body.style.backgroundColor = document.getElementById("bgColor").value;
    }

    displayExpenses();
</script>
</body>
</html>
