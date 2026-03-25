1. Crie o ambiente virtual e instale o Flask 


 ```bash
python3 -m venv venv
 ```

2. Ative o ambiente virtual:
Windows: .\venv\Scripts\activate.
Linux/macOS: 

 ```
source venv/bin/activate
 ```

Instale o Flask: 
 ```
pip install Flask
 ```

2. Crie o arquivo do aplicativo (app.py) 
Crie um arquivo chamado app.py no diretório do projeto.
Adicione o seguinte código ao app.py:

3. Execute o aplicativo
No terminal, dentro do diretório do projeto, digite o comando para rodar o servidor Flask: 
 ```
python3 -m flask run
 ```

Código mínimo
 ```
 from flask import Flask

# Cria uma instância da aplicação Flask
app = Flask(__name__)

# Define uma rota para a página inicial (/)
@app.route('/')
def hello():
    # Retorna a mensagem "Hello, World!"
    frase = 'Hello, World!.yyccyy'
    frase2 = frase
    return frase2

# Executa o servidor de desenvolvimento quando o script é executado
if __name__ == '__main__':
    app.run(debug=True)

```
