<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cadastro de Folga Funcionários</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f8f9fa;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .form-container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
        }
        .form-container h2 {
            margin-bottom: 20px;
            color: #333;
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            font-size: 16px;
        }
        .checkbox-group {
            display: flex;
            flex-direction: column;
        }
        button {
            background: #673ab7;
            color: white;
            border: none;
            padding: 10px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            width: 100%;
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
            <div class="form-group">
                <label>Filial</label>
                <div class="checkbox-group">
                    <label><input type="checkbox" name="filial" value="ARTUR"> ARTUR</label>
                    <label><input type="checkbox" name="filial" value="FLORIANO"> FLORIANO</label>
                    <label><input type="checkbox" name="filial" value="JOTA"> JOTA</label>
                    <label><input type="checkbox" name="filial" value="MODA"> MODA</label>
                    <label><input type="checkbox" name="filial" value="PONTO"> PONTO</label>
                </div>
            </div>
            <div class="form-group">
                <label>Motivo da Folga</label>
                <div class="checkbox-group">
                    <label><input type="checkbox" name="motivo" value="DOMINGO"> DOMINGO</label>
                    <label><input type="checkbox" name="motivo" value="FERIADO"> FERIADO</label>
                    <label><input type="checkbox" name="motivo" value="OUTROS"> OUTROS</label>
                </div>
            </div>
            <button type="submit">Enviar</button>
        </form>
    </div>
</body>
</html>
