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
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            margin: 0;
            padding: 0;
            position: relative;
            overflow-x: hidden;
        }
        .form-container {
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 600px;
            margin-top: 20px;
        }
        .form-container h2 {
            font-size: 24px;
            font-weight: bold;
            color: #202124;
            margin-bottom: 20px;
            text-align: center;
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
        .radio-group label, .select-group select, .date-group input {
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
        .radio-group label:hover, .select-group select:hover, .date-group input:hover {
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
        .hering-logo {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 60px;
            height: auto;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <h2>CADASTRO DE FOLGA FUNCIONÁRIOS</h2>
        <form>
            <fieldset class="form-group">
                <legend>Filial</legend>
                <div class="radio-group" id="filialGroup">
                    <label><input type="radio" name="filial" value="ARTUR"> ARTUR</label>
                    <label><input type="radio" name="filial" value="FLORIANO"> FLORIANO</label>
                    <label><input type="radio" name="filial" value="JOTA"> JOTA</label>
                    <label><input type="radio" name="filial" value="MODA"> MODA</label>
                    <label><input type="radio" name="filial" value="PONTO"> PONTO</label>
                </div>
            </fieldset>

            <fieldset class="form-group">
                <legend>Motivo da Folga</legend>
                <div class="radio-group">
                    <label><input type="radio" name="motivo" value="DOMINGO"> DOMINGO</label>
                    <label><input type="radio" name="motivo" value="FERIADO"> FERIADO</label>
                    <label><input type="radio" name="motivo" value="OUTROS"> OUTROS</label>
                </div>
            </fieldset>

            <fieldset class="form-group">
                <legend>Funcionário</legend>
                <div class="select-group">
                    <select id="funcionario" name="funcionario">
                        <option value="">Selecione a filial primeiro</option>
                    </select>
                </div>
            </fieldset>

            <fieldset class="form-group">
                <legend>Data da Folga</legend>
                <div class="date-group">
                    <input type="date" id="dataFolga" name="dataFolga" required>
                </div>
            </fieldset>

            <button type="submit">Enviar</button>
        </form>
    </div>
    
    <!-- Logo da Hering -->
    <img class="hering-logo" src="https://upload.wikimedia.org/wikipedia/commons/7/7d/Logo_Hering_2019.svg" alt="Hering Logo">

    <script>
        // Função para pegar parâmetros da URL
        function getUrlParameter(name) {
            const urlParams = new URLSearchParams(window.location.search);
            return urlParams.get(name);
        }

        const funcionariosPorFilial = {
            "ARTUR": ["FERNANDA", "LUCILENE"],
            "FLORIANO": ["FERNANDA", "IOLANDA", "MEIRE", "SARA", "THACIANE"],
            "JOTA": ["BRUNO", "VERA"],
            "MODA": ["ANA CLARA", "DAYANE", "JÉSSICA", "JOSY", "LAYANE", "MARIA"],
            "PONTO": ["DANIELA", "MATHEUS", "PAULA", "PRISCILA", "SANDY", "SÔNIA"]
        };
        
        document.querySelectorAll("input[name='filial']").forEach(radio => {
            radio.addEventListener("change", function() {
                const filialSelecionada = this.value;
                const selectFuncionario = document.getElementById("funcionario");
                selectFuncionario.innerHTML = "<option value=''>Selecione o Funcionário</option>";  // Clear the current options
                
                if (funcionariosPorFilial[filialSelecionada]) {
                    const funcionariosOrdenados = funcionariosPorFilial[filialSelecionada].sort((a, b) => a.localeCompare(b, 'pt-BR'));
                    funcionariosOrdenados.forEach(nome => {
                        const option = document.createElement("option");
                        option.value = nome;
                        option.textContent = nome;
                        selectFuncionario.appendChild(option);
                    });
                }
            });
        });

        // Preencher o formulário com os valores da URL
        window.addEventListener("load", function() {
            const filialParam = getUrlParameter('filial');
            const motivoParam = getUrlParameter('motivo');

            if (filialParam) {
                document.querySelector(`input[name="filial"][value="${filialParam}"]`).checked = true;
                const selectFuncionario = document.getElementById("funcionario");
                selectFuncionario.innerHTML = "<option value=''>Selecione o Funcionário</option>";
                
                if (funcionariosPorFilial[filialParam]) {
                    const funcionariosOrdenados = funcionariosPorFilial[filialParam].sort((a, b) => a.localeCompare(b, 'pt-BR'));
                    funcionariosOrdenados.forEach(nome => {
                        const option = document.createElement("option");
                        option.value = nome;
                        option.textContent = nome;
                        selectFuncionario.appendChild(option);
                    });
                }
            }

            if (motivoParam) {
                document.querySelector(`input[name="motivo"][value="${motivoParam}"]`).checked = true;
            }
        });
    </script>
</body>
</html>
