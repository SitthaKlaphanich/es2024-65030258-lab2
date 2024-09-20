<!DOCTYPE html>
<html lang="en"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Express CRUD API Test</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        h1 {
            color: #333;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        input[type="text"] {
            width: calc(100% - 50px);
            padding: 12px;
            margin-right: 5px;
            margin-bottom: 10px;
            border-radius: 4px;
            border: 1px solid #ccc;
        }
        button {
            padding: 12px 20px;
            margin-bottom: 10px;
            background: #5cb85c;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background: #4cae4c;
        }
        .item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 10px 0;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 4px;
        }
        .item input[type="text"] {
            width: calc(50% - 80px);
            margin-right: 5px;
            padding: 10px;
        }
    </style>
    <script>
        let items = [];

        async function fetchItems() {
            const response = await fetch('http://localhost:3000/api/items');
            items = await response.json();
            renderItems();
        }

        function renderItems() {
            const itemsList = document.getElementById('items');
            itemsList.innerHTML = '';
            items.forEach(item => {
                itemsList.innerHTML += `
                    <div class="item">
                        <span>${item.name}</span>
                        <input type="text" placeholder="Update name" id="update-${item._id}" />
                        <button onclick="updateItem('${item._id}')">Update</button>
                        <button onclick="deleteItem('${item._id}')">Delete</button>
                    </div>
                `;
            });
        }

        async function addItem() {
            const firstName = document.getElementById('new-first-name').value;
            const lastName = document.getElementById('new-last-name').value;
            const fullName = `${firstName} ${lastName}`;
            await fetch('http://localhost:3000/api/items', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ name: fullName })
            });
            document.getElementById('new-first-name').value = '';
            document.getElementById('new-last-name').value = '';
            fetchItems();
        }

        async function updateItem(id) {
            const updatedName = document.getElementById(`update-${id}`).value;
            await fetch(`http://localhost:3000/api/items/${id}`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ name: updatedName })
            });
            fetchItems();
        }

        async function deleteItem(id) {
            await fetch(`http://localhost:3000/api/items/${id}`, {
                method: 'DELETE'
            });
            fetchItems();
        }
    </script>
</head>
<body>
    <div class="container">
        <h1>Express CRUD API Test</h1>
        <button onclick="fetchItems()">Fetch Items</button>
        <div>
            <input id="new-first-name" type="text" placeholder="Enter first name">
            <input id="new-last-name" type="text" placeholder="Enter last name">
            <button onclick="addItem()">Add Item</button>
        </div>
        <div id="items">
                    <div class="item">
                        <span>Sittha Klaphanich</span>
                        <input type="text" placeholder="Update name" id="update-66ed61d37bcb0d21f22c43a7">
                        <button onclick="updateItem('66ed61d37bcb0d21f22c43a7')">Update</button>
                        <button onclick="deleteItem('66ed61d37bcb0d21f22c43a7')">Delete</button>
                    </div>
            </div>
    </div>
</body>
</html>
