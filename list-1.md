# Lista 1

## 1. No modelo de referência TCP/IP, descreva as seguintes camadas: Física, Enlace, Rede, Transporte e Aplicação.

A camada de aplicação agrupo as aplicações de rede e seus protocolos. Um protocolo da camada de aplicação é implementado em diversas sistemas finais e possibilita a troca de pacotes de dados (conhecidos como mensagens) entre eles. O HTTP possibilita a troca de documentos e é utilizado por browsers web, o SMTP possibilita a troca de mensagens de correio e é utilizado por agentes de usuário e servidores de e-mail e o FTP permite a troca de arquivos entre sistemas finais.

A camada de transporte é responsável por encapsular a mensagem de aplicação e os seus dados de cabeçalho em um segmento que deve ser transportado até a aplicação de destino. Assim, a camada de transporte mantém uma conexão entre o processo no cliente (origem) e o processo no servidor (destino). Para isso, o protocolo TCP fornece um serviço orientado para a conexão, ou seja, realiza um procedimento de apresentação entre os processos antes de iniciar a troca de dados em si. Esse protocolo disponibiliza de serviços que asseguram a entrega dos dados da aplicação com segurança no destino. Além disso, o TCP fragmenta mensagens longas em segmentos curtos e implementa controle de fluxo e congestionamento.

A camada de rede é responsável por enviar o pacote de dados da camada de transporte do hospedeiro de origem até o hospedeiro de destino. Para isso, a camada de rede encapsula o segmento e o endereço de destino (fornecidos pela camada de transporte) em um datagrama e fornece um serviço de melhor esforço para transmití-lo até o destino final. Existe apenas um protocolo na camada de rede da internet: o protocolo IP. Esse protocolo contém dois componentes importantes. O primeiro componente define os campos do datagrama, cujos campos possibilitam a comunicação entre os enlaces e sistemas finais que receberão o datagrama. O segundo componente é responsável por definir o protocolo de roteamento dos datagramas.

Um datagrama IP é transmitido por uma rota (série de roteadores) desde a origem até o destino final. Assim, a camada de enlace é responsável por rotear o datagrama IP de um nó até o próximo na rota. A camada de enlace provê diversos protocolos como Ethernet, WiFi e PPP (point-to-point protocol). Cada enlace implementa um protocolo específico, sendo assim, é possível que um pacote de dados (conhecido como frame - quadro) seja manipulado por diferentes protocolos de enlace até chegar na camada de rede de destino.

A camada física, mais baixa na pilha de camada, é responsável pela movimentação dos bits individuais dos frames da camada de enlace. Os protocolos dessa camada estão relacionados com o meio de transporte físico. Assim, para cada protocolo de enlace (por exemplo, o Ethernet) existem diversos protocolos de camada física, onde cada protocolo define o modo como os bits serão movimentados.

## 2. O que são sockets?

Os sockets são interfaces que ligam a camada de aplicação e a camada de transporte utilizando um número de porta lógica. Assim, eles são usados para a comunicação entre processos. Uma mensagem de aplicação passa pelo socket para chegar na camada de transporte cliente que irá transmitir a mensagem até o socket do processo de destino.

## 3. Como define-se o protocolo de transporte que uma aplicação necessita?

O protocolo de transporte é definido com base nos recursos requisitados pela aplicação de rede. As aplicações que exijam serviços orientados para conexão, com garantia de entrega de todos os dados, controle de fluxo e congestionamento, devem optar pelo protocolo TCP. Já as aplicações que permitam certa perda de dados, com um serviço não orientado para a conexão, em troca de maior agilidade na troca dos pacotes de dados, devem optar pelo UDP.

## 4. Descreva a arquitetura cliente / servidor.

A arquitetura cliente-servidor é caracterizada por um hospedeiro central que utiliza uma aplicação de rede para trocar mensagens com múltiplas aplicações de rede dos hospedeiros clientes. Para existir a comunicação entre os processos, os hospedeiros implementam o mesmo protocolo de camada de aplicação. Por exemplo, um servidor web (servidor HTTP) recebe requisições e envia respostas utilizando o protocolo HTTP para diversos browsers web (clientes HTTP). Dessa forma, a aplicação servidora deve permanecer sempre ligada enquanto as aplicações clientes não necessariamente.

## 5. Como funciona o protocolo HTTP? Quais são os 2 tipos principais de requisição?

O HTTP é um protocolo de camada de aplicação distribuído entre sistemas finais. Um cliente HTTP utiliza um nome de hospedeiro (*hostname*, para identificar o destino) e um método para enviar uma requisição HTTP ao servidor HTTP que, após processar a requisição, retorna uma resposta HTTP contendo primordialmente o documento requisitado (se ocorrer tudo certo) e um código de status. O HTTP utiliza o TCP como protocolo de transporte. Assim, o processo cliente HTTP (browser) estabelece uma conexão TCP com o processo servidor HTTP (servidor Web) para trocar mensagens. Sempre que o browser pretende requisitar uma página do servidor, ele utiliza a interface socket para passar a mensagem ao TCP que a entrega ao socket do processo do servidor HTTP.

Os dois principais tipos de requisição são GET e POST. Um requisição do tipo GET indica que o cliente HTTP está querendo acessar (requisitar, recuperar) alguma informação contida no servidor HTTP e possivelmente passa alguns parâmetros para isso. Já uma requisição do tipo POST indica que o cliente HTTP está querendo armazenar alguma informação, contida na própria requisição, no servidor HTTP. 

## 6. Cite e descreva 5 códigos de status de resposta do HTTP.

1. **200 ok**: indica que a requisição do cliente foi atendida com sucesso.
2. **301 moved permanently**: indica que o conteúdo requisitado pelo cliente foi movido para outro caminho dentro do servidor.
3. **404 not found**: indica que o conteúdo requisitado pelo cliente não existe no servidor.
4. **500 internal server error**: indica que ocorreu algum erro interno no servidor ao processar a requisição do cliente.
5. **505 HTTP version not supported**: indica que a versão HTTP do cliente não é compatível com a versão implementada no servidor.

## 7. O que é Caching Web ?

Caching Web é o procedimento de utilizar um servidor (proxy) intermediário para receber requisições direcionadas ao servidor Web de origem. O servidor de cache possui um disco de armazenamento local com o intuito de manter objetos do servidor de origem. Assim, quando um cliente HTTP faz uma requisição ao servidor Web, a mensagem passa primeiramente pelo servidor proxy que procura pelo(s) objeto(s) requisitado(s) em seu disco local. Se o conteúdo estiver à disposição do cache, ele envia uma resposta HTTP ao cliente com o conteúdo requisitado. Caso contrário, o servidor de cache estabelece uma conexão TCP com o servidor de origem e solicita (através de uma requisição HTTP) os objetos requisitados pelo cliente. Após o servidor de origem encaminhar uma resposta HTTP contendo o objeto, o servidor proxy armazena-o em seu disco local (para futuras utilizações) e repassa a resposta HTTP ao cliente.

## 8. Descreva o protocolo FTP.

O FTP é um protocolo de camada de aplicação que utiliza o TCP como protocolo de camada de transporte. O FTP é utilizado para a transferência de arquivos entre um hospedeiro local, rodando o processo cliente FTP, e um hospedeiro remoto, rodando o processo servidor FTP. Para isso, o hospedeiro local, através de um agente de usuário FTP (por exemplo, FileZilla), adiciona um nome de hospedeiro para identificar o remoto e assim é estabelecida uma conexão TCP com o processo servidor FTP. Em seguida, o cliente FTP envia dados de autenticação: identificação e senha. Assim que autenticado pelo servidor FTP, o cliente pode iniciar o envio de arquivos do sistema local para o remoto, bem como ler, alterar e remover arquivos do sistema de arquivos remoto. Diferente do HTTP, o FTP estabelece duas conexões TCP paralelas. Uma conexão de controle para os dados de autenticação e comandos para trabalhar com arquivos e uma conexão de dados para os arquivos em si.

## 9. No contexto do SMTP, descreva o que são: Agentes de usuário e Servidores de correio.

Um agente de usuário é uma aplicação de rede utilizada para criar, visualizar, responder e retransmitir mensagens de correio através do protocolo SMTP. As mensagens encaminhadas por um agente de usuário são direcionadas para o seu servidor de correio, no qual elas permanecem na fila de mensagens para serem encaminhadas para as respectivas caixas postais. Para isso, o agente de usuário estabece uma conexão TCP com o servidor de correio remetente e realiza a troca de dados.

Um servidor de correio é uma aplicação de rede utilizada para armazenar e administrar mensagens de correio através do protocolo SMTP. Após receber a mensagem de um agente de usuário, o servidor de correio remetente é responsável por repassar a mensagem da sua fila de mensagens até a caixa postal do destinatário para que o agente de usuário de destino possa ter acesso. Para se conectar com o servidor de correio de destino, o servidor remetente utiliza o protocolo TCP.

## 10. Com funciona o protocolo SMTP, para que um e-mail enviado de uma fonte chegue até seu destino

Para descrever como um e-mail enviado de uma fonte chega até o seu destino, vamos utilizar uma sequência de passos:

1. O usuário 1 deseja enviar um e-mail para o usuário 2. Para isso, ele utiliza um agente de usuário de preferência para compor sua menagem de correio e encaminhá-la utilizando majoritariamente o protocolo SMTP. A mensagem SMTP contendo os dados do remetente, destinatário e corpo da mensagem de correio deve ser direcionada primeiramente para o servidor de correio remetente, do usuário 1. Assim, o agente de usuário remetente estabelece uma conexão TCP com o seu servidor de correio e realiza a troca de dados.

2. Após receber a mensagem do seu agente de usuário, o servidor de correio remetente aloca a mensagem na sua fila de mensagens para repassá-la, assim que possível, para a caixa postal do servidor de correio destinatário. No momento certo, o servidor remetente tenta estabelecer uma conexão TCP com o servidor de correio de destino. Caso a tentativa de conexão falhe, por alguma indisposição do servidor destinário, o remetente manterá a mensagem na fila para novas tentativas no futuro. Se ocorrer tudo certo, o servidor de correio remetente encaminha, utilizando o protocolo SMTP, a mensagem de correio para o servidor de correio destinatário.

3. Quando chega no servidor de correio destinatário, a mensagem é alocada na caixa postal. Agora, usuário 2 já pode utilizar o seu agente de usuário para visualizar, retransmitir e/ou excluir a mensagem de correio vinda do usuário 1.

## 11. Descreva POP3 e IMAP. Qual a principal diferença entre esses dois protocolos?

O POP3 é um protocolo de camada de aplicação utilizado por agentes de usuário para acessar mensagens de correio disponíveis no servidor de correio. Para isso, o agente de usuário estabelece uma conexão TCP com o servidor de correio e inicia a troca de dados. Uma sessão POP3 é dividida em 3 partes: autorização, transação e atualização. Na primeira fase, o agente de usuário envia os dados de identificação e senha do usuário. Na segunda fase, o agente de usuário recupera as mensagens e pode marcar aquelas que devem ser apagadas. Na última fase, o agente de usuário envia o comando `quit` para encerrar a sessão e o servidor de correio pode remover as mensagens marcadas.

O IMAP, assim como o POP3, é um protocolo de camada de aplicação utilizado por agentes de usuários para acessar mensagens disponíveis no servidor de correio. O IMAP é caracterizado por ser mais complexo e, consequentemente, conter mais recursos que o POP3. Diferentemente do POP3, o IMAP possibilita a criação e alocamento de mensagens de correio em pastas no servidor. Outro recurso adicional é a possibilidade de recuperação de componentes de mensagens, tais como cabeçalho, remetente ou parte do corpo da mensagem.
