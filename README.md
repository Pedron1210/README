from flask import Flask, jsonify, request 

app = Flask(__name__)
livros = [
    {
        "id":1,
        "livro" : "harry potter"
    },
    {
        "id":2,
        "livro" : "Romeu e Julieta"
    },
    {
        "id":3,
        "livro" : "Pequeno Principe"
    }
    ]

@app.route('/livros', methods=['GET'])
def consultar_livros(): 
    return jsonify(livros)

@app.route('/livros', methods=['GET'])
def consultar_livros_por_id(id):
    for livro in livros:
        if livro.get('id') == id:
            return jsonify(livro)

@app.route('/livros', methods=['POST'])
def cadastrar_livros():
    novo_livro = request.get_json()
    livros.append(novo_livro)
    return jsonify(livros)

@app.route('/livros/<int:id>', methods=['PUT'])
def atualizar_por_id(id):
    livro_atualizado = request.get_json()
    for indice,livro in enumerate (livros):
        if livro.get('id') == id:
            livros[indice].update(livro_atualizado)
            return jsonify (livros[indice])

@app.route('/livros/<int:id>', methods=['DELETE'])
def excluir_usuario_por_id(id):
    for indice,livro in enumerate (livros):
        if livro.get('id') == id:
         del livro[indice]
        return jsonify(livros[indice])


app.run(port=8080,host='localhost',debug=True)