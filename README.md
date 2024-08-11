yerel-secim-sonuclari/
│
├── index.html
├── style.css
└── script.js
<indexhtml>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2024 Yerel Seçim Sonuçları</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>2024 Yerel Seçim Sonuçları</h1>
    </header>

    <main>
        <div id="map-container">
            <img src="MapChart_Map.png" alt="2024 Türkiye Yerel Seçim Haritası" id="election-map">
            <div id="info-box">
                <!-- Şehir bilgileri burada gösterilecek -->
            </div>
        </div>
    </main>

    <footer>
        <p>&copy; 2024 - Kurgusal Seçim Sonuçları. Tüm Hakları Saklıdır.</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
    text-align: center;
}

header {
    background-color: #4CAF50;
    color: white;
    padding: 10px 0;
}

main {
    padding: 20px;
}

#map-container {
    position: relative;
    display: inline-block;
}

#election-map {
    width: 100%;
    max-width: 800px;
    height: auto;
}

#info-box {
    position: absolute;
    background-color: rgba(255, 255, 255, 0.9);
    border: 1px solid #ccc;
    padding: 10px;
    display: none;
    max-width: 200px;
    z-index: 10;
    border-radius: 5px;
}

footer {
    background-color: #333;
    color: white;
    padding: 10px 0;
    position: fixed;
    bottom: 0;
    width: 100%;
}
document.addEventListener('DOMContentLoaded', function() {
    const map = document.getElementById('election-map');
    const infoBox = document.getElementById('info-box');

    const electionResults = {
        "İstanbul": {
            "winner": "CHP",
            "percentage": "48.80%",
            "logo": "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/CHP_logo.svg/1200px-CHP_logo.svg.png"
        },
        "Ankara": {
            "winner": "CHP",
            "percentage": "50.93%",
            "logo": "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/CHP_logo.svg/1200px-CHP_logo.svg.png"
        },
        "İzmir": {
            "winner": "CHP",
            "percentage": "58.10%",
            "logo": "https://upload.wikimedia.org/wikipedia/commons/thumb/f/f6/CHP_logo.svg/1200px-CHP_logo.svg.png"
        },
        "Bursa": {
            "winner": "AKP",
            "percentage": "49.62%",
            "logo": "https://upload.wikimedia.org/wikipedia/commons/thumb/8/8e/Akparti_logo.png/1200px-Akparti_logo.png"
        },
        // Diğer şehirler ve sonuçları
    };

    map.addEventListener('mousemove', function(event) {
        const x = event.clientX;
        const y = event.clientY;

        const city = getCityFromCoordinates(x, y);
        if (city && electionResults[city]) {
            const result = electionResults[city];
            infoBox.style.display = 'block';
            infoBox.style.left = x + 'px';
            infoBox.style.top = y + 'px';
            infoBox.innerHTML = `
                <strong>${city}</strong><br>
                Kazanan: ${result.winner}<br>
                Oy Oranı: ${result.percentage}<br>
                <img src="${result.logo}" alt="${result.winner} logosu" width="50">
            `;
        } else {
            infoBox.style.display = 'none';
        }
    });

    function getCityFromCoordinates(x, y) {
        // Haritadaki koordinatlara göre şehir belirleme
        // Burada basit bir fonksiyon örneği var. Harita üzerinde her şehir için
        // belirli bir koordinat aralığı atanmalıdır. 

        // Örnek:
        if(x > 100 && x < 200 && y > 50 && y < 150) return "İstanbul";
        if(x > 200 && x < 300 && y > 150 && y < 250) return "Ankara";
        return null;
    }
});
