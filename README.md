# LEXER
import re

# Definir tokens utilizando expresiones regulares
tokens = [
    ('OPEN_PAREN', r'\('),
    ('CLOSE_PAREN', r'\)'),
]

# Función que realiza el análisis léxico
def lexer(expression):
    # Inicializar la lista de tokens vacía
    token_list = []

    # Iterar a través de las expresiones regulares y encontrar coincidencias en la expresión
    for token_name, pattern in tokens:
        regex = re.compile(pattern)
        match = regex.match(expression)

        while match:
            # Agregar el token encontrado a la lista de tokens
            token_value = match.group()
            token_list.append((token_name, token_value))

            # Actualizar la expresión eliminando el token ya encontrado
            expression = expression[len(token_value):]
            match = regex.match(expression)

    # Retornar la lista de tokens
    return token_list

# Ejemplo de uso del lexer
expression = "((()))"
result = lexer(expression)
print(result)
