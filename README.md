<!DOCTYPE html>
<html>
<head>
    <title>Buscador de Futbolistas</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: #f4f4f4; }
        h1 { color: #2ecc71; margin-top: 20px; }
        input, button { margin: 10px; padding: 10px; font-size: 16px; }
        #resultados { margin-top: 20px; font-size: 18px; }
    </style>
</head>
<body>
    <h1>Buscador de Futbolistas</h1>
    <input type="text" id="searchInput" placeholder="Ingresa el nombre del jugador">
    <button onclick="buscarJugador()">Buscar</button>
    <p id="resultados">Esperando búsqueda...</p>

    <script>
        async function buscarJugador() {
            let input = document.getElementById("searchInput").value.toLowerCase();
            let url = `https://api.football-data.org/v4/players?name=${input}`;
            
            try {
                let response = await fetch(url, {
                    headers: { "X-Auth-Token": "TU_API_KEY_AQUÍ" } // Obtén una API Key en Football Data
                });
                let data = await response.json();
                
                let resultadoTexto = data.players.length > 0 
                    ? data.players.map(j => `<b>${j.name}</b> - ${j.team.name} (${j.nationality})<br>Goles: ${j.goals}, Asistencias: ${j.assists}`).join("<br><hr>")
                    : "No se encontraron jugadores.";
                
                document.getElementById("resultados").innerHTML = resultadoTexto;
            } catch (error) {
                document.getElementById("resultados").innerHTML = "Error al obtener datos.";
            }
        }
    </script>
</body>
</html>
