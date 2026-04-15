<!DOCTYPE html><html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TurnitoArg</title>
  <style>
    body { font-family: Arial; margin:0; background:#0f172a; color:white; }
    header { background:#22c55e; padding:15px; text-align:center; font-size:24px; font-weight:bold; }
    .container { padding:20px; }
    .card { background:#1e293b; padding:15px; margin:10px 0; border-radius:10px; }
    input, select, button {
      padding:10px; margin:5px 0; width:100%; border-radius:8px; border:none;
    }
    button { background:#22c55e; color:white; cursor:pointer; }
  </style>
</head>
<body><header>⚽ TurnitoArg</header><div class="container">
  <h2>Crear Partido</h2>
  <input type="text" id="nombre" placeholder="Tu nombre">
  <input type="text" id="ubicacion" placeholder="Ubicación (ej: Mercedes)">
  <input type="date" id="fecha">
  <button onclick="crearPartido()">Publicar Partido</button>  <h2>Partidos Disponibles</h2>
  <select id="filtro" onchange="mostrarPartidos()">
    <option value="todos">Todas las ubicaciones</option>
  </select>  <div id="lista"></div>
</div><script>
  let partidos = [];

  function crearPartido() {
    const nombre = document.getElementById('nombre').value;
    const ubicacion = document.getElementById('ubicacion').value;
    const fecha = document.getElementById('fecha').value;

    if (!nombre || !ubicacion || !fecha) {
      alert('Completa todos los campos');
      return;
    }

    partidos.push({ nombre, ubicacion, fecha });
    actualizarFiltro();
    mostrarPartidos();
  }

  function actualizarFiltro() {
    const filtro = document.getElementById('filtro');
    const ubicaciones = [...new Set(partidos.map(p => p.ubicacion))];

    filtro.innerHTML = '<option value="todos">Todas las ubicaciones</option>';

    ubicaciones.forEach(u => {
      const option = document.createElement('option');
      option.value = u;
      option.textContent = u;
      filtro.appendChild(option);
    });
  }

  function mostrarPartidos() {
    const lista = document.getElementById('lista');
    const filtro = document.getElementById('filtro').value;

    lista.innerHTML = '';

    partidos
      .filter(p => filtro === 'todos' || p.ubicacion === filtro)
      .forEach(p => {
        const div = document.createElement('div');
        div.className = 'card';
        div.innerHTML = `
          <strong>${p.ubicacion}</strong><br>
          📅 ${p.fecha}<br>
          👤 Organiza: ${p.nombre}
        `;
        lista.appendChild(div);
      });
  }
</script></body>
</html># laughing-funicular
