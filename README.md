<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Amigo Secreto</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            padding: 20px;
        }
        #container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
            width: 300px;
            margin: auto;
        }
        ul {
            list-style: none;
            padding: 0;
        }
        li {
            margin: 5px 0;
        }
        button {
            margin-top: 10px;
            padding: 10px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            background-color: #007bff;
            color: white;
            font-size: 16px;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

    <div id="container">
        <h2>Amigo Secreto</h2>
        <input type="text" id="nome" placeholder="Digite o nome">
        <button onclick="adicionarNome()">Adicionar</button>
        <ul id="lista"></ul>
        <button onclick="sortear()" id="botaoSortear">Sortear</button>
        <h3>Resultado:</h3>
        <ul id="resultado"></ul>
    </div>

    <script>
        let participantes = [];

        function adicionarNome() {
            let nomeInput = document.getElementById("nome");
            let nome = nomeInput.value.trim();

            if (nome === "") {
                alert("Digite um nome válido.");
                return;
            }

            if (participantes.includes(nome)) {
                alert("Este nome já foi adicionado.");
                return;
            }

            participantes.push(nome);
            atualizarLista();
            nomeInput.value = "";
        }

        function atualizarLista() {
            let lista = document.getElementById("lista");
            lista.innerHTML = "";
            participantes.forEach(nome => {
                let li = document.createElement("li");
                li.textContent = nome;
                lista.appendChild(li);
            });
        }

        function sortear() {
            if (participantes.length < 2) {
                alert("Adicione pelo menos 2 participantes.");
                return;
            }

            let sorteio = [...participantes]; // Clonando a lista
            let resultado = [];
            let embaralhado = [...sorteio];

            // Embaralha a lista para evitar que a pessoa tire ela mesma
            do {
                embaralhado.sort(() => Math.random() - 0.5);
            } while (embaralhado.some((nome, i) => nome === sorteio[i]));

            for (let i = 0; i < sorteio.length; i++) {
                resultado.push(${sorteio[i]} → ${embaralhado[i]});
            }

            mostrarResultado(resultado);
        }

        function mostrarResultado(resultado) {
            let listaResultado = document.getElementById("resultado");
            listaResultado.innerHTML = "";
            resultado.forEach(par => {
                let li = document.createElement("li");
                li.textContent = par;
                listaResultado.appendChild(li);
            });
        }
    </script>

</body>
</html>
