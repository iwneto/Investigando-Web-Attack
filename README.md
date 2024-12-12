# Investigando Web Attack

O caso a ser investigado será de um log obtido de um servidor que sofreu um ataque recentemente - Desafio dado por LetsDefend (recomendado clicar nas imagens para melhor compreensão)

>O arquivo dos Logs podem ser encontrados na máquina virtual da plataforma, segue abaixo a análise e a resolução das questões:

**1) Qual ferramenta de verificação automatizada o invasor usou para reconhecimento da web?**

![Captura de tela 2024-12-12 124019](https://github.com/user-attachments/assets/dea0fffb-a405-4d37-9671-d4e473820978)

Observa-se na linha 89, no campo user-agent, que a ferramenta usada pelo atacante foi o **Nikto**, um scanner de vulnerabilidades usado para escanear servidores web em busca de arquivos, programas desatualizados, dentre outros.

**2) Após a atividade de reconhecimento da web, qual técnica o invasor usou para descobrir a listagem de diretórios?**

![Captura de tela 2024-12-12 132520](https://github.com/user-attachments/assets/498a2f7b-5b2f-47bd-96e9-d55f9825dff8)

Foi identificado no log, que havia vários nomes de diretórios que o invasor tentou acessar usando uma ferramenta automatizada. No entanto, foi encontrado um código de status 400, significando um erro do lado do cliente, logo dizendo que os diretórios não existem.
Respondendo a questão, a técnica usada pelo atacante foi o **Directory Brute Force (Força Bruta de Diretórios)**.

**3)Qual é o terceiro tipo de ataque após a descoberta da listagem de diretórios?**

![Captura de tela 2024-12-12 143827](https://github.com/user-attachments/assets/0c75d97a-c59f-4dd4-9de2-741e709607b3)

É evidente que o atacante tentou enviar um formulário de login, pois era uma solicitação POST, como pode ser vista nos logs. A tentativa não teve nenhum retorno, pois os tamanhos de resposta eram todos semelhantes, apenas pelo código ser 200.
(Isso significa que o servidor está respondendo com sucesso (200 OK), mas não está fornecendo a resposta esperada, como um redirecionamento para uma página protegida ou uma mensagem de erro indicando falha no login.)

A resposta para essa pergunta é **Brute Force**. Mesmo o nome sendo parecido com a resposta da pergunta número 2, essa técnica visa tentar combinações possíveis de entradas, como chaves e senhas. Já a da pergunta número 2, o ataque Brute Force de diretórios ataca servidores web em específico, tentando adivinhar os nomes de diretórios ou arquivos não visíveis através de requisições HTTP.

**4) O terceiro ataque foi bem-sucedido?**
![Captura de tela 2024-12-12 143827](https://github.com/user-attachments/assets/a734d374-59f4-4d60-9ef9-8ff947c2a21b)

O invasor recebeu constantemente o código de status 200 e um tamanho de resposta similar a 4.086, indicando falta de sucesso. Porém, na linha 12.546 vemos que o invasor encontrou um código 302, que o redirecionou para a página do portal, na mesma linha vemos também o 
código 200 e um tamanho de resposta maior de 23.369, sugerindo um Brute Force bem-sucedido. Logo, a resposta para a questão é **sim**.

**5) Qual é o nome do quarto ataque?**

![Captura de tela 2024-12-12 143907](https://github.com/user-attachments/assets/ccab6411-7bf8-4883-9c1a-33ff86af3c3c)
![ae](https://github.com/user-attachments/assets/ff042fb9-e020-406e-aa5b-6357cfc07ff9)

Como vemos na linha 12.553, a primeira carga útil do quarto ataque, o "whoami". Em primeira análise, supostamente concluiu-se que se tratava de command injection, após muitas pesquisas e erros, foi descoberto a possibilidade de ser **code injection**.

**6) Qual é a primeira carga útil para o 4º ataque?**

Resposta: "whoami"

**7) Há alguma pista de persistência para a máquina vítima no arquivo de log? Se sim, qual é o payload relacionado?**

![ra](https://github.com/user-attachments/assets/cfa39b23-9f89-4707-9dcb-2075c232d87d)

Na linha 12.556, se decodificarmos **%27net%20user%20hacker%20asd123!!%20/add%27** da base64, ele nos dará 'net user hacker asd123!! /add'

>Para finalizar, quaisquer dúvidas, estou a disposição no <a href= "https://www.linkedin.com/in/iwnetoo/">LinkedIn!</a>
