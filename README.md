# Stronkimoj
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lista Zakupów</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        h1 {
            text-align: center;
        }
        #items {
            list-style-type: none;
            padding: 0;
        }
        li {
            background-color: #fff;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        li button {
            background-color: #f44336;
            border: none;
            color: white;
            padding: 5px 10px;
            cursor: pointer;
            border-radius: 5px;
        }
        li button:hover {
            background-color: #d32f2f;
        }
        #new-item {
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        #add-btn {
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            width: 100%;
        }
        #add-btn:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>

    <h1>Wspólna Lista Zakupów</h1>
    <input type="text" id="new-item" placeholder="Dodaj przedmiot...">
    <button id="add-btn">Dodaj do listy</button>
    
    <ul id="items"></ul>

    <script>
        // Pobieranie listy przedmiotów z localStorage
        let items = JSON.parse(localStorage.getItem('items')) || [];

        // Funkcja renderująca listę
        function renderList() {
            const itemsList = document.getElementById('items');
            itemsList.innerHTML = ''; // Czyszczenie listy

            items.forEach((item, index) => {
                const li = document.createElement('li');
                li.innerHTML = `${item} <button onclick="removeItem(${index})">Usuń</button>`;
                itemsList.appendChild(li);
            });
        }

        // Funkcja dodająca przedmiot
        function addItem() {
            const newItemInput = document.getElementById('new-item');
            const newItem = newItemInput.value.trim();

            if (newItem !== '') {
                items.push(newItem);
                localStorage.setItem('items', JSON.stringify(items)); // Zapisanie do localStorage
                newItemInput.value = ''; // Czyszczenie pola tekstowego
                renderList(); // Ponowne renderowanie listy
            }
        }

        // Funkcja usuwająca przedmiot
        function removeItem(index) {
            items.splice(index, 1); // Usunięcie przedmiotu z tablicy
            localStorage.setItem('items', JSON.stringify(items)); // Zapisanie do localStorage
            renderList(); // Ponowne renderowanie listy
        }

        // Nasłuchiwanie kliknięcia przycisku "Dodaj do listy"
        document.getElementById('add-btn').addEventListener('click', addItem);

        // Nasłuchiwanie Enter w polu tekstowym
        document.getElementById('new-item').addEventListener('keydown', function (e) {
            if (e.key === 'Enter') {
                addItem();
            }
        });

        // Renderowanie listy na stronie
        renderList();
    </script>

</body>
</html>
