# To-Do-Listv5
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Entregadas</title>
  <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Rajdhani:wght@400;700&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 2rem;
      font-family: 'Rajdhani', sans-serif;
      background: linear-gradient(to right, #1f4037, #99f2c8);
      color: #fff;
      text-align: center;
      min-height: 100vh;
      position: relative;
    }

    h2 {
      font-family: 'Pacifico', cursive;
      font-size: 2.5rem;
      margin-bottom: 2rem;
      color: #ffe600;
      text-shadow: 2px 2px #000;
    }

    .entregada {
      background-color: rgba(255, 255, 255, 0.1);
      margin: 1rem auto;
      padding: 1rem 2rem;
      border-radius: 12px;
      max-width: 600px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      opacity: 0.8;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
    }

    .entregada button {
      background-color: #ff6b6b;
      color: white;
      border: none;
      padding: 0.4rem 1rem;
      border-radius: 6px;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .entregada button:hover {
      background-color: #ff3b3b;
    }

    .volver-btn {
      margin-top: 2rem;
      padding: 0.7rem 1.5rem;
      background-color: #ffe600;
      color: #333;
      font-weight: bold;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .volver-btn:hover {
      background-color: #ffdd00;
    }

    .confetti {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      pointer-events: none;
      background: url('https://tinyurl.com/confetti-image') center/cover no-repeat;
      animation: fadeIn 2s forwards;
      opacity: 0;
      z-index: 0;
    }

    @keyframes fadeIn {
      to { opacity: 0.25; }
    }
  </style>
</head>
<body>
  <h2>Tareas Entregadas</h2>
  <div id="entregadas"></div>
  <a href="https://charlillos.github.io/To-Do-Listv3/"><button>Volver</button>

  <script>
    const cont = document.getElementById("entregadas");
    const tareas = JSON.parse(localStorage.getItem("tareas") || "[]");

    tareas
      .filter(t => t.entregada)
      .forEach(t => {
        const div = document.createElement("div");
        div.className = "entregada";
        const span = document.createElement("span");
        span.textContent = `[${t.materia}] - ${t.tarea} (${t.fecha})`;

        const del = document.createElement("button");
        del.textContent = "Eliminar";
        del.onclick = () => {
          const rem = JSON.parse(localStorage.getItem("tareas"));
          const nf = rem.filter(a =>
            !(a.materia === t.materia && a.tarea === t.tarea && a.fecha === t.fecha)
          );
          localStorage.setItem("tareas", JSON.stringify(nf));
          location.reload();
        };

        div.appendChild(span);
        div.appendChild(del);
        cont.appendChild(div);
      });

    if (cont.children.length) {
      const conf = document.createElement("div");
      conf.className = "confetti";
      document.body.appendChild(conf);
      new Audio("https://tinyurl.com/applause-sound").play();
    }
  </script>
</body>
</html>
