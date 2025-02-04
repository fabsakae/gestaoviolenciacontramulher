# gestaoviolenciacontramulher
import sqlite3

# Conectar ao banco de dados (ou criar um novo)
conn = sqlite3.connect('violencia_contra_mulher.db')

# Criar um cursor
cursor = conn.cursor()

# Criar uma tabela
cursor.execute('''
CREATE TABLE IF NOT EXISTS casos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    nome TEXT NOT NULL,
    idade INTEGER,
    tipo_violencia TEXT NOT NULL,
    data_ocorrencia TEXT NOT NULL,
    descricao TEXT
)
''')

# Função para inserir dados
def inserir_caso(nome, idade, tipo_violencia, data_ocorrencia, descricao):
    cursor.execute('''
    INSERT INTO casos (nome, idade, tipo_violencia, data_ocorrencia, descricao)
    VALUES (?, ?, ?, ?, ?)
    ''', (nome, idade, tipo_violencia, data_ocorrencia, descricao))
    conn.commit()

# Exemplo de inserção de dados
inserir_caso('Maria Silva', 30, 'Física', '2023-10-01', 'Agressão física por parceiro.')
inserir_caso('Ana Souza', 25, 'Psicológica', '2023-10-02', 'Ameaças e humilhações constantes.')

# Consultar os dados inseridos
cursor.execute('SELECT * FROM casos')
casos = cursor.fetchall()

# Exibir os casos
for caso in casos:
    print(caso)

# Fechar a conexão
conn.close()
