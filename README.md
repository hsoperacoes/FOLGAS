<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Folga Funcionários</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0ebf8;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden; /* Previne rolagem excessiva */
        }
        .form-container {
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 600px;
            box-sizing: border-box; /* Garante que o padding não afete o tamanho */
        }
        .form-container h2 {
            font-size: 24px;
            font-weight: bold;
            color: #202124;
            margin-bottom: 20px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group legend {
            font-size: 16px;
            font-weight: bold;
            color: #5f6368;
            margin-bottom: 10px;
        }
        .radio-group label, .select-group select {
            display: block;
            font-size: 14px;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #dadce0;
            margin-bottom: 8px;
            cursor: pointer;
            background: #fff;
            transition: all 0.3s;
        }
        .radio-group label:hover, .select-group select:hover {
            background: #f1f3f4;
        }
        input[type="radio"] {
            margin-right: 10px;
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
            background: #5a2ea5;
        }
        .error-message {
            color: red;
            font-size: 14px;
            margin-top: 10px;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <h2>CADASTRO DE FOLGA FUNCIONÁRIOS</h2>
        <form id="form">
            <fieldset class="form-group">
                <legend>Filial</legend>
                <div class="radio-group" id="filialGroup">
                    <label><input type="radio" name="filial" value="ARTUR"> ARTUR</label>
                    <label><input type="radio" name="filial" value="FLORIANO"> FLORIANO</label>
                    <label><input type="radio" name="filial" value="JOTA"> JOTA</label>
                    <label><input type="radio" name="filial" value="MODA"> MODA</label>
                    <label><input type="radio" name="filial" value="PONTO"> PONTO</label>
                </div>
                <div class="error-message" id="filialError"></div>
            </fieldset>
            <fieldset class="form-group">
                <legend>Funcionário</legend>
                <div class="select-group">
                    <select id="funcionario" name="funcionario">
                        <option value="">Selecione a filial primeiro</option>
                    </select>
                </div>
                <div class="error-message" id="funcionarioError"></div>
            </fieldset>
            <fieldset class="form-group">
                <legend>Motivo da Folga</legend>
                <div class="radio-group">
                    <label><input type="radio" name="motivo" value="DOMINGO"> DOMINGO</label>
                    <label><input type="radio" name="motivo" value="FERIADO"> FERIADO</label>
                    <label><input type="radio" name="motivo" value="OUTROS"> OUTROS</label>
                </div>
                <div class="error-message" id="motivoError"></div>
            </fieldset>
            <fieldset class="form-group">
                <legend>Data da Folga</legend>
                <input type="date" id="dataFolga" name="dataFolga">
                <div class="error-message" id="dataFolgaError"></div>
            </fieldset>
            <button type="submit">Enviar</button>
        </form>
    </div>
    
    <script>
        const funcionariosPorFilial = {
            "ARTUR": ["LUCILENE", "FERNANDA"],
            "FLORIANO": ["MEIRE", "IOLANDA", "FERNANDA", "THACIANE", "SARA"],
            "JOTA": ["BRUNO", "VERA"],
            "MODA": ["DAYANE", "LAYANE", "JOSY", "MARIA", "JÉSSICA", "ANA CLARA"],
            "PONTO": ["SÔNIA", "SANDY", "PAULA", "MATHEUS", "PRISCILA", "DANIELA"]
        };
        
        document.querySelectorAll("input[name='filial']").forEach(radio => {
            radio.addEventListener("change", function() {
                const filialSelecionada = this.value;
                const selectFuncionario = document.getElementById("funcionario");
                selectFuncionario.innerHTML = "<option value=''>Selecione o funcionário</option>";
                
                if (funcionariosPorFilial[filialSelecionada]) {
                    funcionariosPorFilial[filialSelecionada].forEach(nome => {
                        const option = document.createElement("option");
                        option.value = nome;
                        option.textContent = nome;
                        selectFuncionario.appendChild(option);
                    });
                }
            });
        });

        // Validação do formulário
        document.getElementById("form").addEventListener("submit", function(event) {
            let valid = true;
            let errorMessage = "";

            // Validando Filial
            const filialSelecionada = document.querySelector("input[name='filial']:checked");
            if (!filialSelecionada) {
                valid = false;
                errorMessage = "Selecione a filial!";
                document.getElementById
