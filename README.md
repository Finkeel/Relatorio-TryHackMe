# Relatório CTF Brooklyn Nine-Nine - TryHackMe

## Objetivo
O desafio consiste em encontrar a User Flag e a Root Flag na máquina Brooklynninenine do TryHackMe.

## Etapas Realizadas

1. **Identificação de Portas Abertas**
   - Utilizei o comando `sudo nmap -A 10.10.58.246` e identifiquei as portas 21, 22 e 80 abertas.
   - A porta 21 permitia login FTP anônimo.
   - ![Prompt do Nmap](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/nmap.png)

2. **Exploração Inicial**
   - Acessando o IP via navegador, podemos ver uma página com uma foto da série e um texto embaixo da imagem, nada muito relevante.
   - ![Página Web ](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/site.png)

3. **Análise de Código Fonte**
   - Verifiquei o código fonte da página web
   - ![Código Fonte da Página](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/codigo-fonte.png)

4. **Exploração do FTP Anônimo**
   - Utilizei `ftp 10.10.58.246` e realizei login anônimo.
   - Listei os arquivos disponíveis com `ls -a` e baixei o arquivo `note_to_jake.txt`.
   - ![Listagem de Arquivos FTP](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/listagem-arquivos-ftp.png)
   - ![Conteúdo de note_to_jake.txt](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/conteudo-note-to-jake.png)

5. **Quebra de Senha com Hydra**
   - Usei Hydra para força bruta na senha de Jake: `hydra -l jake -P rockyou.txt 10.10.58.246 ssh -t 16 --VV`.
   - A senha "987654321" foi descoberta.

6. **Acesso via SSH com Credenciais de Jake**
   - Loguei via SSH: `ssh jake@10.10.58.246` utilizando as credenciais encontradas.

7. **Obtendo a User Flag**
   - Identifiquei os usuários com `ls` e encontrei a pasta do usuário "holt".
   - Acessei a pasta e encontrei o arquivo `user.txt` com a User Flag.
   - ![User Flag - user.txt](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/userflag.png)

8. **Escalação de Privilégios para Acesso a Root Flag**
   - Verifiquei as permissões do usuário Jake com `sudo -l` e identifiquei o comando "less".
   - Utilizei `sudo /usr/bin/less /etc/profile` para escalar privilégios.
   - Usei `!/bin/sh` no prompt do less para me tornar root.
   - ![Acesso como root](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/acessoaoroot.png)
   - Acessando o diretório root com `cd /root` podemos pegar a última flag.
   - ![Root Flag](https://github.com/Finkeel/Relatorio-TryHackMe/blob/main/imagens/rootflag.png)

## Flags Encontradas
- User Flag: `ee11cbb19052e40b07aac0ca060c23ee`
- Root Flag: `63a9f0ea7bb98050796b649e85481845`

## Conclusão
O CTF Brooklyn Nine-Nine foi concluído com sucesso, demonstrando habilidades de enumeração, exploração e escalonamento de privilégios para obtenção das flags.

## Vídeo de Resolução
Assista à resolução completa da máquina [aqui](https://www.youtube.com/watch?v=9KDVDI_iyBU).

## Assinatura
[Gustavo Almeida]
[09/01/2024]
