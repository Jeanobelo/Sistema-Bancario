class ContaBancaria:
    def __init__(self, numero, titular, saldo_inicial=0.0):
        self.numero = numero
        self.titular = titular
        self.saldo = saldo_inicial

    def depositar(self, valor):
        if valor > 0:
            self.saldo += valor
            print(f"Depósito de {valor:.2f} realizado com sucesso. Saldo atual: {self.saldo:.2f}")
        else:
            print("O valor do depósito deve ser positivo.")

    def sacar(self, valor):
        if valor > 0:
            if valor <= self.saldo:
                self.saldo -= valor
                print(f"Saque de {valor:.2f} realizado com sucesso. Saldo atual: {self.saldo:.2f}")
            else:
                print("Saldo insuficiente para o saque.")
        else:
            print("O valor do saque deve ser positivo.")

    def consultar_saldo(self):
        print(f"Saldo atual: {self.saldo:.2f}")

    def __str__(self):
        return f"Conta {self.numero} - Titular: {self.titular}, Saldo: {self.saldo:.2f}"


class Banco:
    def __init__(self):
        self.contas = {}

    def criar_conta(self, numero, titular, saldo_inicial=0.0):
        if numero not in self.contas:
            self.contas[numero] = ContaBancaria(numero, titular, saldo_inicial)
            print(f"Conta criada com sucesso: {self.contas[numero]}")
        else:
            print("Número da conta já existe.")

    def buscar_conta(self, numero):
        return self.contas.get(numero, None)

    def depositar(self, numero, valor):
        conta = self.buscar_conta(numero)
        if conta:
            conta.depositar(valor)
        else:
            print("Conta não encontrada.")

    def sacar(self, numero, valor):
        conta = self.buscar_conta(numero)
        if conta:
            conta.sacar(valor)
        else:
            print("Conta não encontrada.")

    def consultar_saldo(self, numero):
        conta = self.buscar_conta(numero)
        if conta:
            conta.consultar_saldo()
        else:
            print("Conta não encontrada.")

    def listar_contas(self):
        for conta in self.contas.values():
            print(conta)


def menu():
    banco = Banco()
    
    while True:
        print("\n--- Sistema Bancário ---")
        print("1. Criar Conta")
        print("2. Depositar")
        print("3. Sacar")
        print("4. Consultar Saldo")
        print("5. Listar Contas")
        print("6. Sair")
        
        escolha = input("Escolha uma opção: ")
        
        if escolha == "1":
            numero = input("Número da conta: ")
            titular = input("Nome do titular: ")
            saldo_inicial = float(input("Saldo inicial (opcional, default 0.0): ") or "0.0")
            banco.criar_conta(numero, titular, saldo_inicial)
        
        elif escolha == "2":
            numero = input("Número da conta: ")
            valor = float(input("Valor a ser depositado: "))
            banco.depositar(numero, valor)
        
        elif escolha == "3":
            numero = input("Número da conta: ")
            valor = float(input("Valor a ser sacado: "))
            banco.sacar(numero, valor)
        
        elif escolha == "4":
            numero = input("Número da conta: ")
            banco.consultar_saldo(numero)
        
        elif escolha == "5":
            banco.listar_contas()
        
        elif escolha == "6":
            print("Saindo do sistema...")
            break
        
        else:
            print("Opção inválida. Tente novamente.")


if __name__ == "__main__":
    menu()
