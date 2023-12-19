Tutorial do Aplicativo de Lista de Tarefas com Arrastar e Soltar
Este é um tutorial passo a passo para entender e usar o aplicativo de lista de tarefas com funcionalidade de arrastar e soltar, desenvolvido em React com TypeScript e usando a biblioteca de arrastar e soltar "@hello-pangea/dnd".

Pré-requisitos
Certifique-se de ter o Node.js instalado em seu sistema antes de prosseguir.

Instalação
Clone este repositório:

bash
Copy code
git clone https://github.com/seu-usuario/seu-repositorio.git
Navegue até o diretório do projeto:

bash
Copy code
cd seu-repositorio
Instale as dependências:

bash
Copy code
npm install
Executando o Aplicativo
Após a instalação, execute o aplicativo com o seguinte comando:

bash
Copy code
npm start
O aplicativo será iniciado e estará disponível em http://localhost:3000.

Entendendo o Código
Vamos dar uma olhada nas principais partes do código.

1. Arquivo App.tsx
   Este arquivo contém o componente principal da aplicação.

Estado:

newTask: Armazena o valor da nova tarefa.
tasks: Armazena a lista de tarefas existente.
Funções Principais:

handleAddTask: Adiciona uma nova tarefa à lista.
reorder: Reordena a lista de tarefas ao arrastar e soltar.
onDragEnd: Chamada quando o arrastar e soltar é concluído. 2. Arquivo task.tsx
Este arquivo contém o componente de Tarefa, utilizado para exibir cada tarefa na lista.

3. Execução do Aplicativo:
   Uma vez iniciado o aplicativo, você verá a interface da lista de tarefas.
   Preencha o campo de texto e clique em "Add" para adicionar uma nova tarefa.
   Arraste e solte as tarefas para reordená-las.
