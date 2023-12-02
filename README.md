# LEXER
import re

# Definir tokens utilizando expresiones regulares
tokens = [
    ('SELECT', r'SELECT'),
    ('FROM', r'FROM'),
    ('WHERE', r'WHERE'),
    ('ORDER_BY', r'ORDER BY'),
    ('LIMIT', r'LIMIT'),
    ('AND', r'AND'),
    ('OR', r'OR'),
    ('IN', r'IN'),
    ('NOT_IN', r'NOT IN'),
    ('OPERATOR', r'=|!=|>|<|>=|<='),
    ('IDENTIFIER', r'[a-zA-Z_][a-zA-Z0-9_]*'),
    ('VALUE', r'\'.*?\'|\d+'),
    ('DELIMITER', r'\(|\)|\[|\]|\{|\}|,'),
    ('ASTERISK', r'\*'),
    ('WHITESPACE', r'\s+'),
]

# Función que realiza el análisis léxico
def lexer(query):
    # Inicializar la lista de tokens vacía
    token_list = []

    # Iterar a través de las expresiones regulares y encontrar coincidencias en la query
    for token_name, pattern in tokens:
        regex = re.compile(pattern)
        match = regex.match(query)

        while match:
            # Agregar el token encontrado a la lista de tokens
            token_value = match.group()
            token_list.append((token_name, token_value))
            query = query[len(token_value):]
            match = regex.match(query)

    return token_list

# Ejemplo de uso del lexer
query = "SELECT * FROM usuarios WHERE nombre = 'Juan'"
result = lexer(query)
print(result)
