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

Para descrever como um e-mail enviado de uma fonte chega até o seu destino, vamos utilizar a seguinte sequência de passos:

1. O usuário 1 deseja enviar um e-mail para o usuário 2. Para isso, ele utiliza um agente de usuário de preferência para compor sua menagem de correio e encaminhá-la utilizando majoritariamente o protocolo SMTP. A mensagem SMTP contendo os dados do remetente, destinatário e corpo da mensagem de correio deve ser direcionada primeiramente para o servidor de correio remetente, do usuário 1. Assim, o agente de usuário remetente estabelece uma conexão TCP com o seu servidor de correio e realiza a troca de dados.

2. Após receber a mensagem do seu agente de usuário, o servidor de correio remetente aloca a mensagem na sua fila de mensagens para repassá-la, assim que possível, para a caixa postal do servidor de correio destinatário. No momento certo, o servidor remetente tenta estabelecer uma conexão TCP com o servidor de correio de destino. Caso a tentativa de conexão falhe, por alguma indisposição do servidor destinário, o remetente manterá a mensagem na fila para novas tentativas no futuro. Se ocorrer tudo certo, o servidor de correio remetente encaminha, utilizando o protocolo SMTP, a mensagem de correio para o servidor de correio destinatário.

3. Quando chega no servidor de correio destinatário, a mensagem é alocada na caixa postal. Agora, usuário 2 já pode utilizar o seu agente de usuário para visualizar, retransmitir e/ou excluir a mensagem de correio vinda do usuário 1.

## 11. Descreva POP3 e IMAP. Qual a principal diferença entre esses dois protocolos?

O POP3 é um protocolo de camada de aplicação utilizado por agentes de usuário para acessar mensagens de correio disponíveis no servidor de correio. Para isso, o agente de usuário estabelece uma conexão TCP com o servidor de correio e inicia a troca de dados. Uma sessão POP3 é dividida em 3 partes: autorização, transação e atualização. Na primeira fase, o agente de usuário envia os dados de identificação e senha do usuário. Na segunda fase, o agente de usuário recupera as mensagens e pode marcar aquelas que devem ser apagadas. Na última fase, o agente de usuário envia o comando `quit` para encerrar a sessão e o servidor de correio pode remover as mensagens marcadas.

O IMAP, assim como o POP3, é um protocolo de camada de aplicação utilizado por agentes de usuários para acessar mensagens disponíveis no servidor de correio. O IMAP é caracterizado por ser mais complexo e, consequentemente, conter mais recursos que o POP3. Diferentemente do POP3, o IMAP possibilita a criação e alocamento de mensagens de correio em pastas no servidor. Outro recurso adicional é a possibilidade de recuperação de componentes de mensagens, tais como cabeçalho, remetente ou parte do corpo da mensagem.

## 12. Como funciona uma consulta a um servidor DNS? Descreva utilizando como é feita a interação entre servidores TLDs e servidores raízes.

Para descrever uma consulta a um servidor DNS, vamos utilizar a seguinte sequência de passos:

1. Suponha que um usuário cliente deseja acessar o website `github.com`. Para isso, ele utiliza um cliente HTTP (browser Web) para montar a requisição com destino a esse nome de hospedeiro. Como os protocolos subjacentes da pilha de camadas não trabalham com nomes de hospedeiros, a camada de aplicação precisa traduzir este para o endereço IP do hospedeiro servidor.

2. Para realizar essa tradução, a camada de aplicação utiliza o sistema de nomes de domínio (DNS). Toda consulta DNS utiliza o UDP como protocolo de transporte. Assim, o cliente DNS do usuário estabelece uma conexão UDP com o servidor DNS local requisitando o endereço IP do hospedeiro servidor de `github.com`.

3. O servidor DNS local, por sua vez, contata um dos servidores DNS raízes. O servidor raiz contactado responderá com um segmento UDP contendo o endereço de um servidor DNS TLD (*top-level domain*) responsável pelo domínio `.com`.

3. Após receber o endereço do servidor DNS TLD, o servidor de nomes local solicita a ele o endereço de um servidor DNS que responde por `github.com`. Logo, o servidor de nomes local recebe o endereço do servidor de nomes com autoridade desejado.

4. Por último, o servidor de nomes local estabelece uma conexão UDP com o servidor de nomes com autoridade solicitando o endereço IP referente a `github.com`. 

5. Quando recebe o endereço IP, o servidor de nomes local o repassa para o cliente DNS do usuário. Agora, o hospedeiro cliente está pronto para continuar com o procedimento de conexão e troca de mensagens com o hospedeiro servidor de `github.com`.

## 13. Descreva como é realizada a consulta repetida (iterativa) e a consulta recursiva.

A consulta repetida (ou iterativa) acontece quando um servidor de nomes estabelece uma sequência de conexões com diferentes servidores DNS em busca da tradução de um nome de hospedeiro. Por exemplo, o servidor de nomes local contacta um servidor DNS raiz, depois um servidor de nomes TLD e, por último, um servidor DNS com autoridade. Assim, o servidor DNS com autoridade responde ao servidor DNS local o endereço IP desejado.

A consulta recursiva acontece quando um servidor de nomes estabelece apenas uma conexão com um servidor de nomes e aguarda a tradução diretamente em seu nome. Por exemplo, um servidor de nomes local estabelece uma conexão com um servidor DNS raiz, o servidor raiz contacta um servidor DNS TLD e o servidor TLD contacta o servidor DNS com autoridade. Assim, como num processo de desempilhamento, o servidor DNS com autoridade responde ao servidor DNS TLD, que repassa ao servidor raiz e este repassa ao servidor de nomes local.

## 14. No contexto do protocolo DNS, descreva os seguintes registros: A, NS, CNAME e MX.

Os registros de recursos servem para o mapeamento de nome de hospedeiro para endereço IP. Cada registro contém 4 campos: `name`, `value`, `type`, `TTL`. O campo `TTL` serve para determinar o tempo de vida que um registro pode se manter em um cache. Esse campo será ignorado a seguir. 

* registro `type=A` 
  * `name`: indica um nome de hospedeiro.
  * `value`: indica o endereço IP referente ao nome de hospedeiro.
  * exemplo: (`website.com`, `1.1.1.1`, `A`).

* registro `type=NS`
  * `name`: indica um nome de hospedeiro.
  * `value`: indica o nome de um servidor DNS com autoridade para o nome de hospedeiro.
  * exemplo: (`website.com`, `dns.website.com`, `NS`).

* registro `type=CNAME`
  * `name`: indica o apelido de hospedeiro. 
  * `value`: indica o nome canônico do apelido de hospedeiro. 
  * exemplo: (`website.com`, `server1.website.com`, `CNAME`)

* registro `type=MX`
  * `name`: indica o apelido de um servidor de correio.
  * `value`: indica o nome canônico do hospedeiro referente ao servidor de correio.
  * exemplo: (`gmail.com`, `mail.gmail.com`, `MX`)

## 15. Qual a importância de ter um servidor DNS “caching only” dentro de uma organização?

Um servidor DNS "caching only" não possui autoridade sobre nenhum domínio, sua função é realizar consultas a outros servidores, armazenar os registros de mapeamento e retornar os resultados. É importante utilizar um servidor "caching only" dentro de uma organização para reduzir o tráfego na rede.

## 16. Quais a diferenças entre as arquiteturas cliente-servidor e P2P?

A arquitetura cliente-servidor é caracterizada por um hospedeiro com o processo servidor, sempre ligado, mantendo conexões com múltiplos hospedeiros com processos clientes. Por outro lado, a arquitetura P2P (peer-to-peer) é caracterizada por conexões diretas entre pares de hospedeiros. Assim, a principal diferença entre as arquiteturas é que a cliente-servidor é centralizada e a P2P é distribuída.

## 17. Descreva os campos dos protocolos TCP e UDP.

Alguns campos são comuns em ambos os protocolos:

* **porta de origem**: indica a porta relacionada ao processo da aplicação de origem. 
* **porta de destino**: indica a porta relacionada ao processo da aplicação de destino.
* **dados de aplicação**: indica a mensagem encapsulada da aplicação (carga útil).

Os campos específicos do UDP são:

* **comprimento**: indica o tamanho total em bytes do segmento UDP, ou seja, o comprimento do cabeçalho mais o comprimento dos dados da aplicação.
* **soma de verificação (*checksum*)**: utilizado para verificar se houve alguma modificação nos bits do segmento durante o transporte.

Os campos específicos do TCP são:

* **número de sequência**: indica o número do primeiro byte do segmento em relação ao conjunto total de dados a ser transportado em uma sessão TCP.
* **número de reconhecimento (*acknowledgment*)**: indica o número do próximo byte esperado por um lado da conexão TCP. 
* **opções**: indica os campos opcionais estabelecidos em uma conexão TCP.
* **janela de recepção**: indica o tamanho máximo aceitável do segmento a ser transportado em um conexão TCP.
* **campo de flag**: indica 6 bits de flags.
* **ponteiro para dados urgentes**: indica o início de um possível conjunto de dados urgentes da aplicação.
* **comprimento do cabeçalho**: indica o comprimento do cabeçalho do TCP, já que o campo de opções pode variar de tamanho.

## 18. Qual a sequência de comandos trocados durante o início de uma conexão TCP?

O protocolo TCP oferece um serviço orientado para a conexão, isto é, sempre que um processo cliente pretender iniciar uma conexão com um processo servidor, as camadas de transporte nos hospedeiros realizarão um procedimento de apresentação antes da troca de dados em si. O procedimento utilizado pelo TCP é conhecido como **apresentação de 3 vias**. 

Suponha que uma aplicação no hospedeiro `A` deseja trocar mensagens com uma aplicação no hospedeiro `B`. Através de um `socket`, o processo de aplicação cliente, rodando no hospedeiro `A`, informa a sua camada de transporte que deseja se conectar com o processo de aplicação `B`, especificado pela porta, que está no hospedeiro `B`, identificado pelo nome de servidor. A sequência de apresentação pode ser descrita como:

1. A camada de transporte em `A` (cliente) envia um segmento TCP especial, sem nenhuma carga útil, para a camada de transporte em `B` (servidor) indicando que pretende estabelecer uma conexão entre o processo cliente em `A` e o processo servidor em `B`. O segmento enviado nessa etapa carrega o bit da flag `SYN` em 1, por isso ele é conhecido como segmento `SYN`.  

2. Em seguida, o servidor opta por aceitar a conexão, aloca os seus recursos (variáveis e buffers) e retorna um segmento TCP especial, também sem carga útil, informando que a conexão pode ser estabelecida. O segmento nessa etapa carrega o bit da flag `SYN` em 1 e um `número de reconhecimento`, por isso ele é conhecido como segmento `SYNACK`.

3. Por último, após receber a resposta positiva (`SYNACK`) do servidor, o cliente também aloca os seus recursos para a conexão e envia um novo segmento TCP especial, podendo conter alguma carga útil, indicando que irá iniciar a troca de dados.

