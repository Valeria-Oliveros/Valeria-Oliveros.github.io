<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Adivina la palabra</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      flex-direction: column;
    }
    #palabra {
      font-size: 24px;
      margin-bottom: 20px;
    }
    button {
      margin-top: 10px;
    }
    #mensaje {
      color: red;
    }
  </style>
</head>
<body>

<h1>Adivina la palabra</h1>

<div id="palabra"></div>
<input type="text" id="letra" maxlength="1">
<button onclick="enviarLetra()">Enviar letra</button>
<p id="intentos"></p>
<p id="mensaje"></p>

<script>
  var palabras = ["GATO", "PERRO", "CASA", "LIBRO", "COCINA", "MESA", "LAPIZ", "ARBOL", "PIZZA", "PLANTA"];
  var palabra;
  var palabraOculta;
  var intentosRestantes = 6;
  var letrasUsadas = [];

  function seleccionarPalabra() {
    palabra = palabras[Math.floor(Math.random() * palabras.length)];
    palabraOculta = "_".repeat(palabra.length);
    document.getElementById("palabra").textContent = palabraOculta;
    document.getElementById("intentos").textContent = "Intentos restantes: " + intentosRestantes;
  }

  function actualizarPalabra(letra) {
    var nuevaPalabraOculta = "";
    for (var i = 0; i < palabra.length; i++) {
      if (palabra[i] === letra) {
        nuevaPalabraOculta += letra;
      } else {
        nuevaPalabraOculta += palabraOculta[i];
      }
    }
    palabraOculta = nuevaPalabraOculta;
    document.getElementById("palabra").textContent = palabraOculta;
  }

  function enviarLetra() {
    var letra = document.getElementById("letra").value.toUpperCase();
    document.getElementById("letra").value = "";
    
    if (letrasUsadas.includes(letra)) {
      document.getElementById("mensaje").textContent = "Ya has usado esa letra. Por favor, elige otra.";
      return;
    }
    
    letrasUsadas.push(letra);

    if (palabra.includes(letra)) {
      actualizarPalabra(letra);
      if (!palabraOculta.includes("_")) {
        document.getElementById("mensaje").textContent = "¡Felicidades! Has adivinado la palabra: " + palabra;
        document.getElementById("intentos").textContent = "";
      }
    } else {
      intentosRestantes--;
      document.getElementById("intentos").textContent = "Intentos restantes: " + intentosRestantes;
      if (intentosRestantes === 0) {
        document.getElementById("mensaje").textContent = "Lo siento, has agotado todos tus intentos. La palabra era: " + palabra;
        document.getElementById("intentos").textContent = "";
      } else {
        document.getElementById("mensaje").textContent = "La letra " + letra + " no está en la palabra.";
      }
    }
  }

  seleccionarPalabra();
</script>

</body>
</html>
