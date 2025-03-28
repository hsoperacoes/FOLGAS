<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Dados Pessoais</title>
    <script>
        function enviarFormulario() {
            const formData = new FormData(document.getElementById("formulario"));
            
            fetch("https://script.google.com/macros/s/AKfycbyogC5qJr9fVW9KTgudFtj0-vhuuo-qfuBTcVAanafbW12kK3W9NsTnjnMtMJAyzUmE/exec", {
                method: "POST",
                body: formData,
            })
            .then(response => response.text())
            .then(data => {
                alert("Dados enviados com sucesso!");
                document.getElementById("formulario").reset();  // Limpa os campos
            })
            .catch(error => alert("Erro ao enviar dados!"));
        }

        function atualizarFuncionarios() {
            const filial = document.getElementById("filial").value;
            const funcionarioSelect = document.getElementById("funcionario");

            // Limpa as opções atuais
            funcionarioSelect.innerHTML = "<option value='' disabled selected>Selecione o Funcionário</option>";

            let funcionarios = [];
            
            // Dependendo da filial, define os funcionários
            if (filial === "ARTUR") {
                funcionarios = ["FERNANDA", "LUCILENE"];
            } else if (filial === "PONTO") {
                funcionarios = ["SANDY", "MATHEUS"];
            } else if (filial === "FLORIANO") {
                funcionarios = ["JOÃO", "ANA"];
            } else if (filial === "JOTA") {
                funcionarios = ["MARCELO", "PAULA"];
            } else if (filial === "MODA") {
                funcionarios = ["CARLOS", "MARIANA"];
            }

            // Preenche a lista de funcionários de acordo com a filial
            funcionarios.forEach(function(funcionario) {
                const option = document.createElement("option");
                option.value = funcionario;
                option.textContent = funcionario;
                funcionarioSelect.appendChild(option);
            });
        }
    </script>
</head>
<body>
    <h2>Formulário de Dados Pessoais</h2>
    <form id="formulario" onsubmit="event.preventDefault(); enviarFormulario();">
        <label>Filial:</label>
        <select id="filial" name="filial" required onchange="atualizarFuncionarios()">
            <option value="" disabled selected>Selecione a Filial</option>
            <option value="ARTUR">ARTUR</option>
            <option value="FLORIANO">FLORIANO</option>
            <option value="JOTA">JOTA</option>
            <option value="MODA">MODA</option>
            <option value="PONTO">PONTO</option>
        </select><br><br>

        <label>Motivo da Folga:</label>
        <select name="motivo_folga" required>
            <option value="DOMINGO">DOMINGO</option>
            <option value="FERIADO">FERIADO</option>
        </select><br><br>

        <label>Funcionário:</label>
        <select id="funcionario" name="funcionario" required>
            <option value="" disabled selected>Selecione o Funcionário</option>
        </select><br><br>
        
        <label>Data de Nascimento:</label>
        <input type="date" name="data_nascimento" required><br><br>
        
        <label>CPF:</label>
        <input type="text" name="cpf" required><br><br>
        
        <button type="submit">Enviar</button>
    </form>
</body>
</html>
