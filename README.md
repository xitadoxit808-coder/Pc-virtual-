import os

class PCVirtual:
    def __init__(self, ram_mb=2048):
        self.ram_total = ram_mb
        self.ram_usada = 0
        self.arquivos = {}
        self.ligado = False

    def ligar(self):
        self.ligado = True
        print("PC virtual ligado. Digite 'ajuda' para ver os comandos.")

    def desligar(self):
        self.ligado = False
        print("PC virtual desligado.")

    def criar_arquivo(self, nome, conteudo=""):
        self.arquivos[nome] = conteudo
        print(f"Arquivo '{nome}' criado.")

    def listar_arquivos(self):
        for nome in self.arquivos:
            print(f"  - {nome}")

    def ler_arquivo(self, nome):
        print(self.arquivos.get(nome, "Arquivo não encontrado."))

    def executar(self, comando):
        partes = comando.split(maxsplit=2)
        acao = partes[0] if partes else ""

        if acao == "ajuda":
            print("Comandos: criar <nome> <texto>, listar, ler <nome>, ram, desligar")
        elif acao == "criar" and len(partes) == 3:
            self.criar_arquivo(partes[1], partes[2])
        elif acao == "listar":
            self.listar_arquivos()
        elif acao == "ler" and len(partes) == 2:
            self.ler_arquivo(partes[1])
        elif acao == "ram":
            print(f"RAM: {self.ram_usada}MB usados de {self.ram_total}MB")
        elif acao == "desligar":
            self.desligar()
        else:
            print("Comando inválido.")

if __name__ == "__main__":
    pc = PCVirtual()
    pc.ligar()
    while pc.ligado:
        pc.executar(input("C:\\> "))
