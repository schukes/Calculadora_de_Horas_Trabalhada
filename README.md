<!DOCTYPE html>
<html>
<head>
  <title>Calculadora de Horas Trabalhadas</title>
  <style>
    body {
      font-family: Arial, sans-serif;
    }

    .container {
      max-width: 500px;
      margin: 0 auto;
      padding: 20px;
      background-color: #f1f1f1;
      border-radius: 5px;
    }

    h1 {
      text-align: center;
    }

    label {
      display: block;
      margin-bottom: 10px;
      font-weight: bold;
    }

    input[type="time"],
    input[type="number"] {
      width: 100%;
      padding: 8px;
      margin-bottom: 20px;
    }

    button {
      display: block;
      width: 100%;
      padding: 10px;
      background-color: #4CAF50;
      color: #fff;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .error {
      color: red;
      margin-top: 10px;
    }

    .result {
      margin-top: 20px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Calculadora de Horas Trabalhadas</h1>

    <label for="horaTrabalhada">Hora Trabalhada:</label>
    <input type="number" id="horaTrabalhada" min="0" step="1" required>

    <label for="inicioPrimeiroPeriodo">Início do Primeiro Período:</label>
    <input type="time" id="inicioPrimeiroPeriodo" required>

    <label for="fimPrimeiroPeriodo">Fim do Primeiro Período:</label>
    <input type="time" id="fimPrimeiroPeriodo" required>

    <label for="inicioSegundoPeriodo">Início do Segundo Período:</label>
    <input type="time" id="inicioSegundoPeriodo" required>

    <label for="fimSegundoPeriodo">Fim do Segundo Período:</label>
    <input type="time" id="fimSegundoPeriodo" required>

    <button onclick="calcularHoras()">Calcular</button>

    <div id="resultado"></div>
  </div>

  <script>
    function calcularHoras() {
      var horaTrabalhada = parseInt(document.getElementById("horaTrabalhada").value);
      var inicioPrimeiroPeriodo = document.getElementById("inicioPrimeiroPeriodo").value;
      var fimPrimeiroPeriodo = document.getElementById("fimPrimeiroPeriodo").value;
      var inicioSegundoPeriodo = document.getElementById("inicioSegundoPeriodo").value;
      var fimSegundoPeriodo = document.getElementById("fimSegundoPeriodo").value;

      var primeiroPeriodoHoras = calcularDiferencaHoras(inicioPrimeiroPeriodo, fimPrimeiroPeriodo);
      var segundoPeriodoHoras = calcularDiferencaHoras(inicioSegundoPeriodo, fimSegundoPeriodo);
      var totalHorasTrabalhadas = primeiroPeriodoHoras + segundoPeriodoHoras + (horaTrabalhada / 60);

      var resultado = document.getElementById("resultado");
      resultado.innerHTML = "";

      if (primeiroPeriodoHoras > 6 || segundoPeriodoHoras > 6 || totalHorasTrabalhadas > 10) {
        resultado.innerHTML += "<p class='error'>Erro: O total de horas trabalhadas excede as regras.</p>";
      } else {
        var horasTrabalhadas = Math.floor(totalHorasTrabalhadas);
        var minutosTrabalhados = Math.round((totalHorasTrabalhadas - horasTrabalhadas) * 60);

        var horasExtras = 0;
        var minutosExtras = 0;

        if (totalHorasTrabalhadas > 8) {
          horasExtras = horasTrabalhadas - 8;
          minutosExtras = minutosTrabalhados;
          horasTrabalhadas = 8;
          minutosTrabalhados = 0;
        }

        resultado.innerHTML += "<p class='result'>Horas trabalhadas: " + formatarHoras(horasTrabalhadas, minutosTrabalhados) + ".</p>";
        resultado.innerHTML += "<p class='result'>Hora extra: " + formatarHoras(horasExtras, minutosExtras) + ".</p>";
      }
    }

    function calcularDiferencaHoras(inicio, fim) {
      var inicioHoras = parseInt(inicio.split(":")[0]);
      var inicioMinutos = parseInt(inicio.split(":")[1]);
      var fimHoras = parseInt(fim.split(":")[0]);
      var fimMinutos = parseInt(fim.split(":")[1]);

      var diferencaHoras = fimHoras - inicioHoras;
      var diferencaMinutos = fimMinutos - inicioMinutos;

      if (diferencaMinutos < 0) {
        diferencaHoras--;
        diferencaMinutos += 60;
      }

      var horas = diferencaHoras + diferencaMinutos / 60;
      return horas;
    }

    function formatarHoras(horas, minutos) {
      return horas.toString().padStart(2, '0') + ':' + minutos.toString().padStart(2, '0');
    }
  </script>
</body>
</html>
