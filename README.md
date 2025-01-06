<!DOCTYPE html>
<html lang="cs">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vyhledávač</title>
</head>
<body>
    <h1>Google Vyhledávání</h1>
    <form id="searchForm">
        <label for="query">Zadejte klíčová slova:</label>
        <input type="text" id="query" name="query" required>
        <button type="submit">Vyhledat</button>
    </form>
    <div id="results"></div>

    <script>
        document.getElementById('searchForm').addEventListener('submit', function (e) {
            e.preventDefault(); // zabrání refresh stranky nikam se to stejně neodesíla je to jen pro test účeli
            const query = document.getElementById('query').value;

            // Simulace výsledků vyhledávání
            const fakeResults = [
                { title: "Výsledek 1", link: "https://www.example1.com", snippet: "Popis výsledku 1." },
                { title: "Výsledek 2", link: "https://www.example2.com", snippet: "Popis výsledku 2." },
                { title: "Výsledek 3", link: "https://www.example3.com", snippet: "Popis výsledku 3." }
            ];

            // Zobrazení výsledků na stránce
            const resultsDiv = document.getElementById('results');
            resultsDiv.innerHTML = "<h2>Výsledky:</h2>";
            fakeResults.forEach(result => {
                const resultItem = document.createElement('div');
                resultItem.innerHTML = `
                    <h3><a href="${result.link}" target="_blank">${result.title}</a></h3>
                    <p>${result.snippet}</p>
                `;
                resultsDiv.appendChild(resultItem);
            });

            // Uložení výsledků do JSON
            saveResults(fakeResults);
        });

        // Funkce pro uložení dat jako JSON toto poradil chat gpt
        const saveResults = (results) => {
            const blob = new Blob([JSON.stringify(results, null, 2)], { type: 'application/json' });
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = 'results.json';
            link.click();
        };
    </script>
</body>
</html>
