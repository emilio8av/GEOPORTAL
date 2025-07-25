<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bienvenido a Nuestro Geoportal</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.css" />
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
            animation: fadeInDown 1s ease-out;
        }

        .header h1 {
            font-size: 3em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
        }

        .geoportal-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            backdrop-filter: blur(10px);
            animation: fadeInUp 1s ease-out 0.3s both;
        }

        .welcome-section {
            text-align: center;
            margin-bottom: 30px;
        }

        .welcome-section h2 {
            color: #333;
            font-size: 2.2em;
            margin-bottom: 15px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .welcome-section p {
            color: #666;
            font-size: 1.1em;
            line-height: 1.6;
            max-width: 600px;
            margin: 0 auto;
        }

        .map-section {
            margin: 30px 0;
        }

        .map-title {
            color: #333;
            font-size: 1.8em;
            margin-bottom: 15px;
            text-align: center;
        }

        #map {
            width: 100%;
            height: 500px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            border: 3px solid #fff;
            animation: mapGlow 2s ease-in-out infinite alternate;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            font-size: 1em;
            cursor: pointer;
            transition: all 0.3s ease;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
        }

        .info-cards {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .card {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            padding: 25px;
            border-radius: 15px;
            color: white;
            text-align: center;
            transform: translateY(0);
            transition: all 0.3s ease;
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }

        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
        }

        .card h3 {
            font-size: 1.5em;
            margin-bottom: 10px;
        }

        .footer {
            text-align: center;
            color: white;
            margin-top: 40px;
            opacity: 0.8;
        }

        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes mapGlow {
            from {
                box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3), 0 0 0 3px #fff;
            }
            to {
                box-shadow: 0 10px 30px rgba(118, 75, 162, 0.3), 0 0 0 3px #fff;
            }
        }

        @media (max-width: 768px) {
            .header h1 {
                font-size: 2em;
            }
            
            .welcome-section h2 {
                font-size: 1.8em;
            }
            
            #map {
                height: 300px;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>¡Bienvenido!</h1>
            <p>Explora el mundo a través de nuestro geoportal interactivo</p>
        </div>

        <div class="geoportal-container">
            <div class="welcome-section">
                <h2>🌍 Un Saludo Espacial</h2>
                <p>Descubre ubicaciones, explora mapas y navega por el mundo desde la comodidad de tu navegador. Nuestro geoportal te permite visualizar datos geográficos de manera intuitiva y moderna.</p>
            </div>

            <div class="map-section">
                <h3 class="map-title">📍 Mapa Mundial</h3>
                <div id="map"></div>
                
                <div class="controls">
                    <button class="btn" onclick="goToLocation(-0.2201641, -78.5123274)">📍 Quito, Ecuador</button>
                    <button class="btn" onclick="goToLocation(40.4168, -3.7038)">📍 Madrid, España</button>
                    <button class="btn" onclick="goToLocation(0, 0)">🌍 Vista Mundial</button>
                    <button class="btn" onclick="addRandomMarker()">➕ Marcador Aleatorio</button>
                </div>
            </div>

            <div class="info-cards">
                <div class="card">
                    <h3>🗺️ Mapas Interactivos</h3>
                    <p>Navegación fluida con zoom y desplazamiento para explorar cualquier región del mundo.</p>
                </div>
                <div class="card">
                    <h3>📌 Marcadores Dinámicos</h3>
                    <p>Añade y personaliza marcadores para identificar ubicaciones importantes.</p>
                </div>
                <div class="card">
                    <h3>🔍 Búsqueda Avanzada</h3>
                    <p>Encuentra lugares específicos con nuestra funcionalidad de búsqueda integrada.</p>
                </div>
            </div>
        </div>

        <div class="footer">
            <p>&copy; 2025 Geoportal. Explorando el mundo juntos. 🌟</p>
        </div>
    </div>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/leaflet.js"></script>
    <script>
        // Inicializar el mapa
        let map = L.map('map').setView([-0.2201641, -78.5123274], 10);

        // Añadir capa de mapa base
        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            maxZoom: 19,
            attribution: '© OpenStreetMap contributors'
        }).addTo(map);

        // Marcador inicial en Quito
        let quitoMarker = L.marker([-0.2201641, -78.5123274])
            .addTo(map)
            .bindPopup('<b>¡Hola desde Quito!</b><br>Capital de Ecuador 🇪🇨')
            .openPopup();

        // Array para almacenar marcadores adicionales
        let markers = [quitoMarker];

        // Función para ir a una ubicación específica
        function goToLocation(lat, lng) {
            if (lat === 0 && lng === 0) {
                map.setView([20, 0], 2);
            } else {
                map.setView([lat, lng], 10);
            }
        }

        // Función para añadir marcador aleatorio
        function addRandomMarker() {
            const cities = [
                {name: "París", lat: 48.8566, lng: 2.3522, flag: "🇫🇷"},
                {name: "Tokyo", lat: 35.6762, lng: 139.6503, flag: "🇯🇵"},
                {name: "Nueva York", lat: 40.7128, lng: -74.0060, flag: "🇺🇸"},
                {name: "Lima", lat: -12.0464, lng: -77.0428, flag: "🇵🇪"},
                {name: "Londres", lat: 51.5074, lng: -0.1278, flag: "🇬🇧"},
                {name: "Río de Janeiro", lat: -22.9068, lng: -43.1729, flag: "🇧🇷"},
                {name: "Bogotá", lat: 4.7110, lng: -74.0721, flag: "🇨🇴"},
                {name: "Buenos Aires", lat: -34.6118, lng: -58.3960, flag: "🇦🇷"}
            ];

            const randomCity = cities[Math.floor(Math.random() * cities.length)];
            
            const newMarker = L.marker([randomCity.lat, randomCity.lng])
                .addTo(map)
                .bindPopup(`<b>${randomCity.name}</b><br>¡Descubriendo el mundo! ${randomCity.flag}`);
            
            markers.push(newMarker);
            map.setView([randomCity.lat, randomCity.lng], 8);
        }

        // Evento de clic en el mapa
        map.on('click', function(e) {
            const customMarker = L.marker([e.latlng.lat, e.latlng.lng])
                .addTo(map)
                .bindPopup(`<b>¡Nuevo punto!</b><br>Lat: ${e.latlng.lat.toFixed(4)}<br>Lng: ${e.latlng.lng.toFixed(4)}`);
            
            markers.push(customMarker);
        });

        // Agregar algunos efectos visuales adicionales
        setTimeout(() => {
            quitoMarker.openPopup();
        }, 1000);
    </script>
</body>
</html>
