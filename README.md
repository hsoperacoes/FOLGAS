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
            height: 100vh; /* Ajustando para altura total da tela */
            overflow: auto; /* Ativa a barra de rolagem quando necessário */
        }
        .form-container {
            background: white;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 600px;
            overflow: auto; /* Garante que o formulário tenha rolagem */
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
        .radio-group label, .select-group select, input[type="date"] {
            display: block;
            font-size: 14px;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #dadce0;
            margin-bottom: 8px;
            cursor: pointer;
            background: #fff;
            transition: all 0.3s;
            width: 100%;
        }
        .radio-group label:hover, .select-group select:hover, input[type="date"]:hover {
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
                <legend>Funcionário</legend>
                <div class="select-group">
                    <select id="funcionario" name="funcionario" disabled>
                        <option value="">Selecione a filial primeiro</option>
                    </select>
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
                <legend>Data da Folga</legend>
                <input type="date" name="data_folga" required>
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
                selectFuncionario.innerHTML = "<option value=''>Selecione o funcionário</option>"; // Reseta as opções

                // Habilita o select de funcionários após selecionar a filial
                selectFuncionario.disabled = false;

                // Adiciona os funcionários da filial selecionada
                if (funcionariosPorFilial[filialSelecionada]) {
                    funcionariosPorFilial[filialSelecionada].sort().forEach(nome => {
                        const option = document.createElement("option");
                        option.value = nome;
                        option.textContent = nome;
                        selectFuncionario.appendChild(option);
                    });
                }
            });
        });
    </script>
</body>
</html>
