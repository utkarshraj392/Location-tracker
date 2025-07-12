# Location-tracker
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Location Tracker</title>
  <link
    rel="stylesheet"
    href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"
  />
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      text-align: center;
    }
    h1 {
      background: #4caf50;
      color: white;
      padding: 10px;
    }
    #map {
      height: 80vh;
      width: 100%;
    }
    #status {
      padding: 10px;
    }
  </style>
</head>
<body>
  <h1>Live Location Tracker</h1>
  <div id="status">Requesting your location...</div>
  <div id="map"></div>

  <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
  <script>
    const status = document.getElementById("status");

    if ("geolocation" in navigator) {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          const lat = position.coords.latitude;
          const lon = position.coords.longitude;

          status.textContent = `Location found: Latitude ${lat.toFixed(5)}, Longitude ${lon.toFixed(5)}`;

          // Show map
          const map = L.map("map").setView([lat, lon], 15);

          L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
            maxZoom: 19,
            attribution: '© OpenStreetMap contributors',
          }).addTo(map);

          L.marker([lat, lon]).addTo(map)
            .bindPopup("You are here.")
            .openPopup();
        },
        (error) => {
          status.textContent = "Error: Location access denied or unavailable.";
        }
      );
    } else {
      status.textContent = "Geolocation is not supported in this browser.";
    }
  </script>
</body>
</html>
