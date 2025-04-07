<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Folga Funcionários</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #121212;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            overflow-y: auto;
            color: #e0e0e0;
        }
        .form-container {
            background: #1e1e1e;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.8);
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
            color: #b39ddb;
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
            border: 1px solid #444;
            margin-bottom: 8px;
            cursor: pointer;
            background: #2c2c2c;
            color: #e0e0e0;
            transition: all 0.3s;
        }
        button {
            background: #673ab7;
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
        input[type="radio"] {
            margin-right: 5px;
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
            "JOTA": ["BRUNO", "CARINA", "DENISE", "FABIOLA","JÉSSICA", "LOUISE", "NATALIA", "PRISCILA", "RAYSSA", "VERA"],
            "MODA": ["ANA CLARA", "DAIANE", "JÉSSICA", "MARCIA", "NAISE", "MARIA"],
            "PONTO": ["DANIELA", "DEBORA", "ISADORA", "PAULA", "PRISCILA", "SANDY", "SÔNIA"]
        };

        document.getElementById('filialGroup').addEventListener('change', function() {
            var filialSelecionada = document.querySelector('input[name="filial"]:checked');
            var funcionarioSelect = document.getElementById('funcionario');
            funcionarioSelect.innerHTML = "<option value=''>Selecione um funcionário</option>";

            if (filialSelecionada) {
                funcionariosPorFilial[filialSelecionada.value].forEach(function(funcionario) {
                    var option = document.createElement("option");
                    option.value = funcionario;
                    option.textContent = funcionario;
                    funcionarioSelect.appendChild(option);
                });
            }
        });

        document.querySelectorAll('input[name="motivo"]').forEach(function(radio) {
            radio.addEventListener('change', function() {
                const dataFolgaInput = document.getElementById("dataFolga");
                const motivoOutrosField = document.getElementById("motivoOutros");
                const dataTrabalhoInput = document.getElementById("dataTrabalho");

                if (!dataTrabalhoInput.value) {
                    alert("Selecione primeiro a Data de Trabalho!");
                    this.checked = false;
                    return;
                }

                let dataTrabalho = new Date(dataTrabalhoInput.value);
                let maxDate = new Date(dataTrabalho);

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

        document.getElementById("form").addEventListener("submit", function(event) {
            event.preventDefault();
            let formData = new FormData(this);

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
