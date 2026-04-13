# Tarefa-1---Publisher-e-Subscriber
Tarefa 1 da RoboFEI - Humanóide (Programação), qual é necessário criar um nó de um publisher e o nó de um subscriber e fazer a comunicação entre ambos através de um tópico.

Criar um publisher e um subscriber no ROS 2 é basicamente configurar dois nós (nodes) que se comunicam por meio de um tópico. O processo começa com a criação de um package dentro do seu workspace (ros2_ws), que será onde todo o código e configurações ficam organizados. Esse package precisa ser configurado com as dependências corretas (como as bibliotecas padrão do ROS 2 para comunicação) e preparado para compilação ou execução, dependendo se você está usando C++ ou Python. Depois disso, você estrutura o projeto criando arquivos separados para o publisher e o subscriber dentro das pastas apropriadas (como src no C++ ou dentro do próprio package no Python).

O próximo passo é configurar o sistema de build. No caso de C++, você ajusta o CMakeLists.txt para registrar os executáveis dos nós e garantir que eles sejam compilados corretamente. Já no Python, você edita o setup.py para declarar os scripts como executáveis do package. Essa etapa é essencial, porque é ela que permite que o ROS 2 reconheça seus nós como comandos executáveis dentro do sistema.

Com tudo configurado, você compila o workspace usando o colcon build e depois ativa o ambiente com o comando source. Isso faz com que o ROS 2 reconheça o novo package e seus executáveis. A partir daí, você já pode rodar o publisher e o subscriber em terminais separados. O publisher será responsável por enviar mensagens para um tópico específico, enquanto o subscriber se conecta a esse mesmo tópico para receber e processar essas mensagens.

Por fim, é importante validar se a comunicação está funcionando corretamente. Isso pode ser feito verificando os tópicos ativos, listando os nós em execução e observando se as mensagens estão sendo transmitidas entre eles. Em resumo, o processo envolve: criar o package, estruturar os arquivos, configurar o build, compilar o workspace e executar os nós — tudo isso sem precisar focar diretamente na implementação do código em si, mas sim na organização e integração dentro do ecossistema do ROS 2.

```mkdir -p ~/ros2_ws/src```
