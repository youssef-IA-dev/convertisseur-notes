<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Convertisseur de Notes</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            padding: 20px;
            text-align: center;
        }
        h1 {
            color: #333;
        }
        input, select {
            padding: 10px;
            margin: 10px 0;
            width: 200px;
        }
        button {
            padding: 10px 15px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            font-size: 1.2em;
            color: #333;
        }
    </style>
</head>
<body>

  <h1>Convertisseur de Notes</h1>
    <label for="note">Entrez votre note (ex: 8/75):</label>
    <input type="text" id="note" placeholder="8/75">
    
  <label for="maxValue">Valeur maximale du système actuel:</label>
    <input type="number" id="maxValue" placeholder="75">
    
  <label for="targetSystem">Système de notation cible:</label>
    <select id="targetSystem">
        <option value="20">Sur 20</option>
        <option value="10">Sur 10</option>
        <option value="percentage">Pourcentage</option>
        <option value="gpa">GPA sur 4</option>
    </select>
    
  <button onclick="convertNote()">Convertir</button>
    
   <div class="result" id="result"></div>

   <script>
        function convertNote() {
            const noteInput = document.getElementById('note').value;
            const maxValue = parseFloat(document.getElementById('maxValue').value);
            const targetSystem = document.getElementById('targetSystem').value;
            const resultDiv = document.getElementById('result');

            // Vérification de la validité de l'entrée
            if (!noteInput.includes('/') || isNaN(maxValue)) {
                resultDiv.innerHTML = "Veuillez entrer une note valide et une valeur maximale.";
                return;
            }

            const [numerator, denominator] = noteInput.split('/').map(Number);
            if (denominator !== maxValue) {
                resultDiv.innerHTML = "La valeur maximale ne correspond pas au dénominateur de la fraction.";
                return;
            }

            // Calcul de la note sur 100
            const scoreOutOf100 = (numerator / denominator) * 100;

            let convertedScore;
            switch (targetSystem) {
                case '20':
                    convertedScore = (scoreOutOf100 / 100) * 20;
                    resultDiv.innerHTML = `Note convertie: ${convertedScore.toFixed(2)} / 20`;
                    break;
                case '10':
                    convertedScore = (scoreOutOf100 / 100) * 10;
                    resultDiv.innerHTML = `Note convertie: ${convertedScore.toFixed(2)} / 10`;
                    break;
                case 'percentage':
                    resultDiv.innerHTML = `Note convertie: ${scoreOutOf100.toFixed(2)} %`;
                    break;
                case 'gpa':
                    convertedScore = (scoreOutOf100 / 100) * 4;
                    resultDiv.innerHTML = `Note convertie: ${convertedScore.toFixed(2)} / 4`;
                    break;
                default:
                    resultDiv.innerHTML = "Système de notation non reconnu.";
            }
        }
    </script>

</body>
</html>
