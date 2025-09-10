<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Examen de Aritmética</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin: 50px;
      background: #f4f9f9;
    }
    .card {
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0px 4px 10px rgba(0,0,0,0.2);
      display: inline-block;
      max-width: 500px;
      width: 100%;
    }
    h1 {
      color: #2b6777;
    }
    button {
      margin: 10px;
      padding: 10px 20px;
      border: none;
      background: #52ab98;
      color: white;
      font-size: 16px;
      border-radius: 8px;
      cursor: pointer;
    }
    button:hover {
      background: #3a7d71;
    }
    input {
      padding: 10px;
      margin-top: 10px;
      width: 120px;
      text-align: center;
      font-size: 18px;
    }
    #resultado {
      margin-top: 15px;
      font-weight: bold;
    }
    .contador {
      margin-top: 20px;
      font-size: 18px;
      color: #333;
    }
    .correcto {
      color: green;
    }
    .incorrecto {
      color: red;
    }
    .final {
      font-size: 20px;
      margin-top: 20px;
      color: #2b6777;
    }
  </style>
</head>
<body>
  <div class="card">
    <h1>Examen de Aritmética</h1>
    <p id="problema">Haz clic en "Iniciar Examen"</p>
    <input type="number" id="respuesta" placeholder="Tu respuesta" disabled>
    <br>
    <button onclick="verificar()" id="btnVerificar" disabled>Verificar</button>
    <button onclick="iniciarExamen()">Iniciar Examen</button>
    <p id="resultado"></p>
    <div class="contador">
      Pregunta: <span id="numPregunta">0</span> / 10<br>
      ✅ Aciertos: <span id="aciertos">0</span><br>
      ❌ Errores: <span id="errores">0</span>
    </div>
    <div class="final" id="final"></div>
  </div>

  <script>
    let numero1, numero2, operador, solucion;
    let aciertos = 0, errores = 0, preguntaActual = 0;
    const totalPreguntas = 10;

    function iniciarExamen() {
      aciertos = 0;
      errores = 0;
      preguntaActual = 0;
      document.getElementById("aciertos").innerText = 0;
      document.getElementById("errores").innerText = 0;
      document.getElementById("numPregunta").innerText = 0;
      document.getElementById("final").innerText = "";
      document.getElementById("respuesta").disabled = false;
      document.getElementById("btnVerificar").disabled = false;
      nuevaOperacion();
    }

    function nuevaOperacion() {
      if (preguntaActual >= totalPreguntas) {
        finalizarExamen();
        return;
      }

      const operadores = ["+", "-", "×", "÷"];
      operador = operadores[Math.floor(Math.random() * operadores.length)];
      numero1 = Math.floor(Math.random() * 20) + 1;
      numero2 = Math.floor(Math.random() * 20) + 1;

      if (operador === "÷") {
        numero1 = numero1 * numero2; // asegurar divisiones exactas
      }

      document.getElementById("problema").innerText = `${numero1} ${operador} ${numero2} = ?`;

      switch (operador) {
        case "+": solucion = numero1 + numero2; break;
        case "-": solucion = numero1 - numero2; break;
        case "×": solucion = numero1 * numero2; break;
        case "÷": solucion = numero1 / numero2; break;
      }

      document.getElementById("resultado").innerText = "";
      document.getElementById("respuesta").value = "";
      preguntaActual++;
      document.getElementById("numPregunta").innerText = preguntaActual;
    }

    function verificar() {
      if (preguntaActual > totalPreguntas) return;

      let respuesta = Number(document.getElementById("respuesta").value);
      let resultado = document.getElementById("resultado");

      if (respuesta === solucion) {
        resultado.innerText = "✅ ¡Correcto!";
        resultado.className = "correcto";
        aciertos++;
        document.getElementById("aciertos").innerText = aciertos;
      } else {
        resultado.innerText = `❌ Incorrecto. La respuesta era ${solucion}`;
        resultado.className = "incorrecto";
        errores++;
        document.getElementById("errores").innerText = errores;
      }

      setTimeout(nuevaOperacion, 1000);
    }

    function finalizarExamen() {
      let porcentaje = Math.round((aciertos / totalPreguntas) * 100);
      document.getElementById("problema").innerText = "Examen finalizado ✅";
      document.getElementById("respuesta").disabled = true;
      document.getElementById("btnVerificar").disabled = true;
      document.getElementById("final").innerText =
        `Resultados: ${aciertos} aciertos, ${errores} errores. Puntaje: ${porcentaje}%`;
    }
  </script>
</body>
</html>
