import random
import datetime
import webbrowser

class Cassandra:
    def __init__(self, nome):
        self.nome = nome
        self.saudacoes = [
            f"Olá! Eu sou {self.nome}, seu assistente virtual. Como posso ajudar?",
            f"Oi! {self.nome} à sua disposição. O que você precisa?",
            f"Pronto para ajudar! Eu sou o {self.nome}."
        ]
        self.despedidas = [
            "Até logo! Estarei aqui se precisar.",
            "Tchau! Volte sempre.",
            "Foi um prazer ajudar. Até mais!"
        ]
        self.comandos = {
            "hora": self.mostrar_hora,
            "data": self.mostrar_data,
            "pesquisar": self.pesquisar_web,
            "aleatório": self.numero_aleatorio,
            "ajuda": self.mostrar_ajuda
        }

    def iniciar(self):
        print(random.choice(self.saudacoes))
        self.mostrar_ajuda()
        self.executar()

    def mostrar_hora(self, _=None):
        hora_atual = datetime.datetime.now().strftime("%H:%M:%S")
        print(f"A hora atual é {hora_atual}")

    def mostrar_data(self, _=None):
        data_atual = datetime.datetime.now().strftime("%d/%m/%Y")
        print(f"Hoje é {data_atual}")

    def numero_aleatorio(self, _=None):
        num = random.randint(1, 100)
        print(f"Seu número aleatório é: {num}")

    def mostrar_ajuda(self, _=None):
        print("\nComandos disponíveis:")
        print("- hora: Mostra a hora atual")
        print("- data: Mostra a data atual")
        print("- pesquisar [termo]: Faz uma pesquisa na web")
        print("- aleatório: Gera um número aleatório entre 1 e 100")
        print("- ajuda: Mostra esta mensagem de ajuda")
        print("- sair: Encerra o assistente\n")

    def pesquisar_web(self, termo=""):
        if not termo:
            print("O que você gostaria que eu pesquisasse?")
            termo = input("> ")
        url = f"https://www.google.com/search?q={termo}"
        webbrowser.open(url)
        print(f"Pesquisando por '{termo}' no navegador...")

    def executar(self):
        while True:
            comando = input("> ").lower().split()
            
            if not comando:
                continue
                
            if comando[0] == "sair":
                print(random.choice(self.despedidas))
                break
                
            if comando[0] in self.comandos:
                acao = self.comandos[comando[0]]
                if len(comando) > 1:
                    acao(" ".join(comando[1:]))
                else:
                    acao()
            else:
                print("Comando não reconhecido. Digite 'ajuda' para ver os comandos disponíveis.")

# Criando e iniciando o assistente
if __name__ == "__main__":
    assistente = Cassandra("Cassandra")
    assistente.iniciar()
