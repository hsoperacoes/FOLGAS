<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Cadastro de Folga Funcionários</title>
  <style>
    :root {
      --bg-color: #121212;
      --card-color: #1e1e1e;
      --text-color: #ffffff;
      --input-bg: #2c2c2c;
      --border-color: #444;
      --highlight-color: #673ab7;
    }

    body {
      font-family: Arial, sans-serif;
      background-color: var(--bg-color);
      color: var(--text-color);
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      overflow-y: auto;
    }

    .form-container {
      background: var(--card-color);
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.5);
      width: 100%;
      max-width: 800px;
      box-sizing: border-box;
    }

    .form-group {
      margin-bottom: 20px;
    }

    .form-group legend {
      font-size: 16px;
      font-weight: bold;
      color: var(--text-color);
      margin-bottom: 10px;
    }

    .radio-group label,
    .select-group select,
    input[type="date"],
    input[type="text"],
    select {
      display: block;
      font-size: 14px;
      padding: 10px;
      border-radius: 4px;
      border: 1px solid var(--border-color);
      margin-bottom: 8px;
      cursor: pointer;
      background: var(--input-bg);
      color: var(--text-color);
      width: 100%;
      box-sizing: border-box;
    }

    option {
      background: var(--input-bg);
      color: var(--text-color);
    }

    button {
      background: var(--highlight-color);
      color: white;
      border: none;
      padding: 12px;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
      width: 100%;
      margin-top: 10px;
      transition: background 0.3s;
    }

    button:hover {
      background: #5e35b1;
    }

    #motivoOutros {
      display: none;
    }

    #filialGroup label,
    #motivoGroup label,
    #funcionarioGroup label {
      display: block;
      margin-bottom: 8px;
    }
  </style>
</head>
<body>
  <div class="form-container">
    <h2>CADASTRO DE FOLGA FUNCIONÁRIOS</h2>
    <form id="form" method="POST" action="https://script.google.com/macros/s/AKfycbwh-YUwL2o3_i-bfcV9RMzLcoI98vyyGwEXf4LHlG5KJ59gIAlUe1_VVlFQMBqU6PwR/exec">
      <fieldset class="form-group" id="filialGroup">
        <legend>Filial</legend>
        <label><input type="radio" name="filial" value="ARTUR"> ARTUR</label>
        <label><input type="radio" name="filial" value="FLORIANO"> FLORIANO</label>
        <label><input type="radio" name="filial" value="JOTA"> JOTA</label>
        <label><input type="radio" name="filial" value="MODA"> MODA</label>
        <label><input type="radio" name="filial" value="PONTO"> PONTO</label>
      </fieldset>

      <fieldset class="form-group" id="funcionarioGroup">
        <legend>Funcionário</legend>
        <select id="funcionario" name="funcionario">
          <option value="">Selecione a filial primeiro</option>
        </select>
      </fieldset>

      <fieldset class="form-group">
        <legend>DIA TRABALHADO</legend>
        <input type="date" id="dataTrabalho" name="dataTrabalho">
      </fieldset>

      <fieldset class="form-group" id="motivoGroup">
        <legend>Motivo da Folga</legend>
        <label><input type="radio" name="motivo" value="DOMINGO"> DOMINGO</label>
        <label><input type="radio" name="motivo" value="FERIADO"> FERIADO</label>
        <label><input type="radio" name="motivo" value="OUTROS"> OUTROS</label>
      </fieldset>

      <fieldset class="form-group" id="motivoOutros">
        <legend>Especificar o Motivo</legend>
        <input type="text" name="outrosMotivo" placeholder="Escreva o motivo">
      </fieldset>

      <fieldset class="form-group">
        <legend>Data da Folga</legend>
        <input type="date" id="dataFolga" name="dataFolga">
      </fieldset>

      <button type="submit">Enviar</button>
    </form>
  </div>

  <script>
    const funcionariosPorFilial = {
      "ARTUR": ["FERNANDA", "LUCILENE"],
      "FLORIANO": ["FERNANDA", "MEIRE", "SARA", "THACIANNE"],
      "JOTA": ["BRUNO", "CARINA", "DENISE", "FABIOLA", "JÉSSICA", "LOUISE", "NATALIA", "PRISCILA", "RAYSSA", "VERA"],
      "MODA": ["ANA CLARA", "DAIANE", "JÉSSICA", "MARCIA", "NAISE", "MARIA"],
      "PONTO": ["DANIELA", "DEBORA", "ISADORA", "PAULA", "PRISCILA", "SANDY", "SÔNIA"]
    };

    document.getElementById('filialGroup').addEventListener('change', function() {
      const filialSelecionada = document.querySelector('input[name="filial"]:checked');
      const funcionarioSelect = document.getElementById('funcionario');
      funcionarioSelect.innerHTML = "<option value=''>Selecione um funcionário</option>";

      if (filialSelecionada) {
        funcionariosPorFilial[filialSelecionada.value].forEach(function(funcionario) {
          const option = document.createElement("option");
          option.value = funcionario;
          option.textContent = funcionario;
          funcionarioSelect.appendChild(option);
        });
      }
    });

    document.querySelectorAll('input[name="motivo"]').forEach(function(radio) {
      radio.addEventListener('change', function () {
        const dataTrabalhoInput = document.getElementById("dataTrabalho");
        const dataFolgaInput = document.getElementById("dataFolga");
        const motivoOutrosField = document.getElementById("motivoOutros");

        if (!dataTrabalhoInput.value) {
          alert("Selecione primeiro a Data de Trabalho!");
          this.checked = false;
          return;
        }

        const dataTrabalho = new Date(dataTrabalhoInput.value);
        const maxDate = new Date(dataTrabalho);

        if (this.value === "DOMINGO") {
          maxDate.setDate(dataTrabalho.getDate() + 7);
        } else if (this.value === "FERIADO") {
          maxDate.setDate(dataTrabalho.getDate() + 30);
        }

        dataFolgaInput.min = dataTrabalho.toISOString().split('T')[0];
        dataFolgaInput.max = maxDate.toISOString().split('T')[0];
        motivoOutrosField.style.display = this.value === "OUTROS" ? "block" : "none";
      });
    });

    document.getElementById("form").addEventListener("submit", function (event) {
      event.preventDefault();
      const formData = new FormData(this);

      fetch(this.action, {
        method: "POST",
        body: formData
      })
        .then(response => response.text())
        .then(data => {
          alert("Folga cadastrada com sucesso!");
          this.reset();
          document.getElementById("funcionario").innerHTML = '<option value="">Selecione a filial primeiro</option>';
        })
        .catch(error => alert("Erro ao enviar os dados!"));
    });
  </script>
</body>
</html>
