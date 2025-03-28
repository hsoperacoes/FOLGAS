<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Formulário de Dados Pessoais</title>
    <script>
        function enviarFormulario() {
            const formData = new FormData(document.getElementById("formulario"));
            
            fetch("https://script.google.com/macros/s/SEU_ID_AQUI/exec", {  // Substitua pelo seu link do Web App
                method: "POST",
                body: formData,
            })
            .then(response => response.text())
            .then(data => alert("Dados enviados com sucesso!"))
            .catch(error => alert("Erro ao enviar dados!"));
        }
    </script>
</head>
<body>
    <h2>Formulário de Dados Pessoais</h2>
    <form id="formulario" onsubmit="event.preventDefault(); enviarFormulario();">
        <label>Nome:</label>
        <input type="text" name="nome" required><br><br>
        
        <label>E-mail:</label>
        <input type="email" name="email" required><br><br>
        
        <label>Telefone:</label>
        <input type="tel" name="telefone" required><br><br>
        
        <label>Data de Nascimento:</label>
        <input type="date" name="data_nascimento" required><br><br>
        
        <label>CPF:</label>
        <input type="text" name="cpf" required><br><br>
        
        <button type="submit">Enviar</button>
    </form>
</body>
</html>
