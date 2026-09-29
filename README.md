TIPOS_COMBUSTIVEL = ("gasolina", "etanol", "diesel")

abastecimentos = []
ids_usados = set()


def ler_float(texto):
    """Lê um número decimal."""
    while True:
        try:
            valor = float(input(texto).replace(",", "."))
            if valor <= 0:
                print("Digite um valor maior que zero.")
            else:
                return valor
        except ValueError:
            print("Valor inválido.")


def ler_int(texto):
    """Lê um número inteiro."""
    while True:
        try:
            return int(input(texto))
        except ValueError:
            print("Digite um número inteiro válido.")


def gerar_id():
    """Gera um ID sem repetir."""
    novo_id = len(ids_usados) + 1

    while novo_id in ids_usados:
        novo_id += 1

    ids_usados.add(novo_id)
    return novo_id


def iniciais(nome):
    """Pega as iniciais do cliente usando slicing."""
    partes = nome.split()
    resultado = ""

    for parte in partes:
        resultado += parte[:1].upper()

    return resultado


def gerador(lista):
    """Percorre os registros com yield."""
    for item in lista:
        yield item


def calcular_total(litros, valor_litro):
    """Calcula o total do abastecimento."""
    return litros * valor_litro


def cadastrar():
    """Cadastra um abastecimento."""
    print("\n--- Cadastrar abastecimento ---")

    cliente = input("Nome do cliente: ").strip()

    if cliente == "":
        print("O nome não pode ficar vazio.")
        return

    print("\nCombustíveis disponíveis:")
    for tipo in TIPOS_COMBUSTIVEL:
        print("-", tipo)

    combustivel = input("Combustível: ").lower().strip()

    if combustivel not in TIPOS_COMBUSTIVEL:
        print("Combustível inválido.")
        return
