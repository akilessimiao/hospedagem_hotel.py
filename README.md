# Sistema de Hospedagem - Gerenciamento de Hotel

# Dicionário para armazenar informações dos quartos
quartos = {
    101: {"tipo": "Solteiro", "preco": 100.0, "ocupado": False},
    102: {"tipo": "Casal", "preco": 150.0, "ocupado": False},
    103: {"tipo": "Luxo", "preco": 300.0, "ocupado": False},
    201: {"tipo": "Solteiro", "preco": 100.0, "ocupado": False},
    202: {"tipo": "Casal", "preco": 150.0, "ocupado": False},
    203: {"tipo": "Luxo", "preco": 300.0, "ocupado": False},
}

# Lista para armazenar informações dos hóspedes
hospedes = []

# Função para exibir quartos disponíveis
def exibir_quartos_disponiveis():
    print("\nQuartos disponíveis:")
    for numero, info in quartos.items():
        if not info["ocupado"]:
            print(f"Quarto {numero}: Tipo - {info['tipo']}, Preço - R${info['preco']:.2f} por noite")
    print()

# Função para reservar um quarto
def reservar_quarto():
    nome = input("Digite o nome do hóspede: ")
    dias = int(input("Digite o número de dias de estadia: "))
    exibir_quartos_disponiveis()
    quarto_escolhido = int(input("Digite o número do quarto desejado: "))

    if quarto_escolhido in quartos and not quartos[quarto_escolhido]["ocupado"]:
        custo_total = quartos[quarto_escolhido]["preco"] * dias
        quartos[quarto_escolhido]["ocupado"] = True
        hospedes.append({"nome": nome, "quarto": quarto_escolhido, "dias": dias, "custo_total": custo_total})
        print(f"\nReserva confirmada para {nome} no quarto {quarto_escolhido} por {dias} dias. Custo total: R${custo_total:.2f}\n")
    else:
        print("\nQuarto indisponível ou inválido. Tente novamente.\n")

# Função para exibir lista de hóspedes
def exibir_hospedes():
    if hospedes:
        print("\nHóspedes atuais:")
        for hospede in hospedes:
            print(f"Nome: {hospede['nome']}, Quarto: {hospede['quarto']}, Dias: {hospede['dias']}, Custo Total: R${hospede['custo_total']:.2f}")
        print()
    else:
        print("\nNenhum hóspede registrado no momento.\n")

# Função para realizar o checkout
def checkout():
    quarto = int(input("Digite o número do quarto para checkout: "))
    for hospede in hospedes:
        if hospede["quarto"] == quarto:
            print(f"\nCheckout realizado para {hospede['nome']}.")
            quartos[quarto]["ocupado"] = False
            hospedes.remove(hospede)
            return
    print("\nQuarto não encontrado ou já está desocupado.\n")

# Menu principal
def menu():
    while True:
        print("=== Sistema de Gerenciamento de Hotel ===")
        print("1. Exibir quartos disponíveis")
        print("2. Reservar quarto")
        print("3. Exibir lista de hóspedes")
        print("4. Realizar checkout")
        print("5. Sair")
        opcao = input("Escolha uma opção: ")

        if opcao == "1":
            exibir_quartos_disponiveis()
        elif opcao == "2":
            reservar_quarto()
        elif opcao == "3":
            exibir_hospedes()
        elif opcao == "4":
            checkout()
        elif opcao == "5":
            print("Encerrando sistema. Até mais!")
            break
        else:
            print("Opção inválida. Tente novamente.\n")

# Inicia o programa
menu()
