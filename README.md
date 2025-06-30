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
