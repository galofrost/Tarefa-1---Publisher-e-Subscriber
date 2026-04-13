# Tarefa-1---Publisher-e-Subscriber
Tarefa 1 da RoboFEI - Humanóide (Programação), qual é necessário criar um nó de um publisher e o nó de um subscriber e fazer a comunicação entre ambos através de um tópico.

Criar um publisher e um subscriber no ROS 2 é basicamente configurar dois nós (nodes) que se comunicam por meio de um tópico. O processo começa com a criação de um package dentro do seu workspace (ros2_ws), que será onde todo o código e configurações ficam organizados. Esse package precisa ser configurado com as dependências corretas (como as bibliotecas padrão do ROS 2 para comunicação) e preparado para compilação ou execução, dependendo se você está usando C++ ou Python. Depois disso, você estrutura o projeto criando arquivos separados para o publisher e o subscriber dentro das pastas apropriadas (como src no C++ ou dentro do próprio package no Python).

O próximo passo é configurar o sistema de build. No caso de C++, você ajusta o CMakeLists.txt para registrar os executáveis dos nós e garantir que eles sejam compilados corretamente. Já no Python, você edita o setup.py para declarar os scripts como executáveis do package. Essa etapa é essencial, porque é ela que permite que o ROS 2 reconheça seus nós como comandos executáveis dentro do sistema.

Com tudo configurado, você compila o workspace usando o colcon build e depois ativa o ambiente com o comando source. Isso faz com que o ROS 2 reconheça o novo package e seus executáveis. A partir daí, você já pode rodar o publisher e o subscriber em terminais separados. O publisher será responsável por enviar mensagens para um tópico específico, enquanto o subscriber se conecta a esse mesmo tópico para receber e processar essas mensagens.

Por fim, é importante validar se a comunicação está funcionando corretamente. Isso pode ser feito verificando os tópicos ativos, listando os nós em execução e observando se as mensagens estão sendo transmitidas entre eles. Em resumo, o processo envolve: criar o package, estruturar os arquivos, configurar o build, compilar o workspace e executar os nós — tudo isso sem precisar focar diretamente na implementação do código em si, mas sim na organização e integração dentro do ecossistema do ROS 2.

Para iniciar a criação de um Publisher e um Subscriber, primeiro é necessário verificar se o ROS2 está devidamente instalado e configurado no seu computador. Para isso, digite o seguinte comando no terminal:  
```bash
source /opt/ros/humble/setup.bash
```

Se o ROS2 estiver corretamente instalado, o terminal apenas avançará para a próxima linha sem exibir mensagens. Caso contrário, será exibido algum erro indicando que a instalação não foi encontrada.

Além disso, é necessário ter o colcon instalado, pois ele será utilizado para criar e compilar pacotes. Normalmente, ele já vem com o ROS2, mas caso não esteja disponível, instale com o comando:
```bash
sudo apt install python3-colcon-common-extensions
```

Com isso pronto, o próximo passo é criar o workspace, que será o ambiente onde seu pacote ficará localizado.

Execute os seguintes comandos:
```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
```

Dentro do diretório src, crie o pacote que conterá o Publisher e o Subscriber:
```bash
ros2 pkg create --build-type ament_python --license Apache-2.0 pub_sub
```
Agora, acesse o diretório do pacote:
```bash
cd ~/ros2_ws/src/pub_sub/pub_sub
```

Em seguida, crie o Publisher com o comando:
```bash
wget https://raw.githubusercontent.com/ros2/examples/humble/rclpy/topics/minimal_publisher/examples_rclpy_minimal_publisher/publisher_member_function.py
```

Ainda nesse mesmo diretório, crie o Subscriber:
```bash
wget https://raw.githubusercontent.com/ros2/examples/humble/rclpy/topics/minimal_subscriber/examples_rclpy_minimal_subscriber/subscriber_member_function.py
```

Depois disso, volte para o diretório principal do pacote:
```bash
cd ~/ros2_ws/src/pub_sub
```

Agora, edite o arquivo package.xml para adicionar as dependências necessárias:
```bash
nano package.xml
```

Logo abaixo das tags de descrição, maintainer e licença, adicione:
```xml
<exec_depend>rclpy</exec_depend>
<exec_depend>std_msgs</exec_depend>
```

Importante: certifique-se de a Descrição, Maintainer e Licença estão exatamente iguais tanto no package.xml quanto no setup.py.

Salve o arquivo (Ctrl + O, depois Enter) e saia (Ctrl + X).

Agora, edite o arquivo setup.py:
```bash
nano setup.py
```

Substitua:

```xml
entry_points={
        'console_scripts': [
        ],
},
```
```xml
Por:

entry_points={
        'console_scripts': [
                'talker = Pubsub.publisher_member_function:main',
                'listener = Pubsub.subscriber_member_function:main',
        ],
},
```

Salve e saia do arquivo.

Com tudo configurado, volte para o diretório raiz do workspace:
```bash
cd ~/ros2_ws
```

Verifique e instale possíveis dependências com:
```bash
rosdep install -i --from-path src --rosdistro humble -y
```

Agora, compile o pacote e configure o ambiente:
```bash
colcon build
source install/setup.bash
```

Tudo está pronto! Para testar, abra um novo terminal, vá até o workspace e ative o ambiente novamente:
```bash
cd ~/ros2_ws
source install/setup.bash
```

Em terminais separados, execute:
```bash
ros2 run pub_sub talker
ros2 run pub_sub listener
```
Se tudo estiver correto, o Publisher (talker) começará a enviar mensagens e o Subscriber (listener) irá recebê-las.
