<!DOCTYPE html>
<html>
<head>
  <title>Calculadora de Horas de Trabalho</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f2f2f2;
    }

    #container {
      max-width: 400px;
      margin: 0 auto;
      padding: 20px;
      background-color: #fff;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    }

    h1 {
      text-align: center;
    }

    label {
      display: block;
      margin-top: 10px;
    }

    input[type="time"] {
      width: 100%;
      padding: 5px;
    }

    input[type="submit"] {
      display: block;
      width: 100%;
      margin-top: 20px;
      padding: 10px;
      background-color: #4CAF50;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .result {
      margin-top: 20px;
      padding: 10px;
      background-color: #f2f2f2;
      border: 1px solid #ddd;
      border-radius: 5px;
    }

    .warning {
      color: #ff0000;
      font-weight: bold;
    }

    .success {
      color: #008000;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div id="container">
    <h1>Calculadora de Horas de Trabalho</h1>
    <form id="work-hours-form">
      <label for="total-hours">Total de Horas Trabalhadas:</label>
      <input type="time" id="total-hours" required>

      <label for="first-period-start">Início do Primeiro Período:</label>
      <input type="time" id="first-period-start" required>

      <label for="first-period-end">Fim do Primeiro Período:</label>
      <input type="time" id="first-period-end" required>

      <label for="second-period-start">Início do Segundo Período:</label>
      <input type="time" id="second-period-start" required>

      <label for="second-period-end">Fim do Segundo Período:</label>
      <input type="time" id="second-period-end" required>

      <input type="submit" value="Calcular">
    </form>

    <div id="results" style="display: none;">
      <div class="result">
        <span id="total-result"></span>
        <span id="total-warning" class="warning"></span>
      </div>
      <div class="result">
        <span id="lunch-result"></span>
        <span id="lunch-warning" class="warning"></span>
      </div>
    </div>
  </div>

  <script>
    document.getElementById("work-hours-form").addEventListener("submit", function(event) {
      event.preventDefault();

      var totalHoursInput = document.getElementById("total-hours").value.split(":");
      var totalHours = parseFloat(totalHoursInput[0]) + (parseFloat(totalHoursInput[1]) / 60);

      var firstPeriodStartInput = document.getElementById("first-period-start").value.split(":");
      var firstPeriodStart = parseFloat(firstPeriodStartInput[0]) + (parseFloat(firstPeriodStartInput[1]) / 60);

      var firstPeriodEndInput = document.getElementById("first-period-end").value.split(":");
      var firstPeriodEnd = parseFloat(firstPeriodEndInput[0]) + (parseFloat(firstPeriodEndInput[1]) / 60);

      var secondPeriodStartInput = document.getElementById("second-period-start").value.split(":");
      var secondPeriodStart = parseFloat(secondPeriodStartInput[0]) + (parseFloat(secondPeriodStartInput[1]) / 60);

      var secondPeriodEndInput = document.getElementById("second-period-end").value.split(":");
      var secondPeriodEnd = parseFloat(secondPeriodEndInput[0]) + (parseFloat(secondPeriodEndInput[1]) / 60);

      var firstPeriodDuration = calculateDuration(firstPeriodStart, firstPeriodEnd);
      var secondPeriodDuration = calculateDuration(secondPeriodStart, secondPeriodEnd);
      var lunchDuration = calculateDuration(firstPeriodEnd, secondPeriodStart);

      var totalDuration = firstPeriodDuration + secondPeriodDuration;

      document.getElementById("total-result").innerText = "Duração Total: " + convertToHours(totalDuration);
      document.getElementById("lunch-result").innerText = "Duração do Almoço: " + convertToHours(lunchDuration);

      if (totalDuration < totalHours) {
        document.getElementById("total-warning").innerText = "Atraso: " + convertToHours(totalHours - totalDuration);
      } else {
        document.getElementById("total-warning").innerText = "Hora Extra: " + convertToHours(totalDuration - totalHours);
      }

      if (firstPeriodDuration > 6) {
        document.getElementById("total-warning").innerText += " | O primeiro período excede 6 horas (Advertência)";
      }

      if (secondPeriodDuration > 6) {
        document.getElementById("total-warning").innerText += " | O segundo período excede 6 horas (Advertência)";
      }

      if (totalDuration > 10) {
        document.getElementById("total-warning").innerText += " | Hora total de expediente > 10 horas (Advertência)";
      }

      if (lunchDuration < 1) {
        document.getElementById("lunch-warning").innerText = "Almoço menor que 1 hora (Advertência)";
      } else if (lunchDuration > 2) {
        document.getElementById("lunch-warning").innerText = "Almoço maior que 2 horas (Advertência)";
      }

      document.getElementById("results").style.display = "block";
    });

    function calculateDuration(start, end) {
      return end >= start ? end - start : (24 - start) + end;
    }

    function convertToHours(duration) {
      var hours = Math.floor(duration);
      var minutes = Math.round((duration - hours) * 60);

      if (minutes === 60) {
        hours++;
        minutes = 0;
      }

      return hours.toString().padStart(2, "0") + ":" + minutes.toString().padStart(2, "0");
    }
  </script>
</body>
</html>
