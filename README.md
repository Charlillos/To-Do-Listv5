# To-Do-Listv5
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Tareas</title>

  <!-- Fuente decorativa y moderna -->
  <link href="https://fonts.googleapis.com/css2?family=Rajdhani:wght@400;700&display=swap" rel="stylesheet">

  <style>
    * {
      box-sizing: border-box;
    }

    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      font-family: 'Rajdhani', sans-serif;
      background-color: #0d1b2a;
      color: #ffffff;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    body::before {
      content: "";
      position: fixed;
      top: 0; left: 0;
      width: 100vw;
      height: 100vh;
      background:
        radial-gradient(circle at 20% 30%, rgba(0, 191, 255, 0.15), transparent 200px),
        radial-gradient(circle at 80% 60%, rgba(255, 105, 180, 0.15), transparent 250px),
        radial-gradient(circle at 50% 80%, rgba(255, 255, 255, 0.1), transparent 150px);
      animation: bgFloat 20s infinite linear;
      z-index: 0;
      pointer-events: none;
    }

    @keyframes bgFloat {
      0% { background-position: 0 0, 0 0, 0 0; }
      100% { background-position: 1000px 1000px, -800px -800px, 500px 500px; }
    }

    .container {
      background: rgba(255, 255, 255, 0.05);
      padding: 3rem;
      border-radius: 12px;
      box-shadow: 0 0 20px rgba(0, 255, 255, 0.2);
      text-align: center;
      width: 90%;
      max-width: 600px;
      z-index: 1;
      position: relative;
    }

    h2 {
      font-size: 2.2rem;
      color: #00d4ff;
      margin-bottom: 1.5rem;
    }

    ul {
      list-style: none;
      padding: 0;
      text-align: left;
    }

    li {
      background-color: rgba(255, 255, 255, 0.08);
      padding: 1rem;
      margin-bottom: 0.8rem;
      border-left: 5px solid #00d4ff;
      border-radius: 6px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    li:first-child {
      border-left-color: #ff5050;
    }

    li span {
      flex: 1;
      margin-right: 1rem;
    }

    button {
      background-color: #00d4ff;
      border: none;
      color: #000;
      padding: 0.5rem 1rem;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #00a8cc;
    }

    .volver {
      margin-top: 2rem;
      background-color: #ff7eb9;
    }

    .volver:hover {
      background-color: #ff4da6;
    }
  </style>
</head>
<body>

  <div class="container">
    <h2>Listado de tareas</h2>
    <ul id="lista"></ul>
    <button class="volver">Volver</button> 
  <button>Siguiente</button>
  </div>

  <script>
    const lista = document.getElementById("lista");
    const tareas = JSON.parse(localStorage.getItem("tareas") || "[]");

    // Ordenar por fecha más próxima
    tareas.sort((a, b) => new Date(a.fecha) - new Date(b.fecha));

    tareas.forEach((t, i) => {
  const li = document.createElement("li");
  const prioridad = i === 0 ? "🔴" : "⏳";
  li.textContent = `${prioridad} [${t.materia}] - ${t.tarea} (${t.fecha})`;

  const btn = document.createElement("button");
  btn.textContent = t.entregada ? "✅" : "Entregada";
  
  btn.onclick = () => {
    tareas[i].entregada = true;
    localStorage.setItem("tareas", JSON.stringify(tareas));
    btn.textContent = "✅"; // Aquí está el cambio clave
  };

  li.appendChild(btn);
  lista.appendChild(li);
});
  </script>

</body>
</html>
