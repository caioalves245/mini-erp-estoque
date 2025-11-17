# mini-erp-estoque
Mini ERP de estoque em Python
# mini_erp_estoque.py

produtos = []

def cadastrar_produto():
    id_produto = len(produtos) + 1
    nome = input("Nome do produto: ")
    categoria = input("Categoria: ") 
    while True:
        try:
            preco = float(input("Preço: "))
            break
        except ValueError:
            print("Digite um valor numérico para o preço.")    
    while True:
        try:
            quantidade = int(input("Quantidade: "))
            break
        except ValueError:
            print("Digite um número inteiro para a quantidade.")
    produto = {
        "id": id_produto,
        "nome": nome,
        "categoria": categoria,
        "preco": preco,
        "quantidade": quantidade
    }
    produtos.append(produto)
    print(f"\n Produto '{nome}' cadastrado com sucesso!\n")

def excluir_produto():
    if not produtos:
        print("Nenhum produto cadastrado.")
        return 
    try:
        id_excluir = int(input("Digite o ID do produto que deseja excluir: "))
    except ValueError:
        print("Digite um número válido.")
        return
    for p in produtos:
        if p["id"] == id_excluir:
            produtos.remove(p)
            print(f"\n Produto '{p['nome']}' excluído!\n")
            return
    print("Produto não encontrado.")

def listar_produtos():
    if not produtos:
        print("Nenhum produto cadastrado.")
        return
    print("\n--- Produtos Cadastrados ---")
    for p in produtos:
        status = " Estoque baixo!" if p["quantidade"] < 5 else ""
        print(f"ID: {p['id']}, Nome: {p['nome']}, Categoria: {p['categoria']}, Preço: R${p['preco']:.2f}, Quantidade: {p['quantidade']} {status}")
    print("----------------------------\n")

def menu():
    while True:
        print("=== Sistema Mini ERP - Estoque ===")
        print("1. Cadastrar produto")
        print("2. Excluir produto")
        print("3. Listar produtos")
        print("4. Sair")  
        opcao = input("Escolha uma opção: ")
        if opcao == "1":
            cadastrar_produto()
        elif opcao == "2":
            excluir_produto()
        elif opcao == "3":
            listar_produtos()
        elif opcao == "4":
            print("Saindo do sistema...")
            break
        else:
            print("Opção inválida! Tente novamente.\n")

if __name__ == "__main__":
    menu()
