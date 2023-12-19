# Tutorial Completo: Criando um Projeto React com Vite, Tailwind CSS e Arrastar e Soltar

### Este tutorial guiará você na criação de um projeto React usando Vite, Tailwind CSS e a funcionalidade de arrastar e soltar utilizando a biblioteca "@hello-pangea/dnd".

### Vamos dividir isso em várias etapas:

### Pré-requisitos

1. Node.js: Certifique-se de ter o Node.js instalado em seu sistema. Você pode baixá-lo em https://nodejs.org/.

### Passo 1: Configuração do Projeto

Criar um novo projeto React usando Vite:

```bash
npx create-vite meu-projeto-react --template react-ts
```

Siga as instruções para criar o projeto.

2. Navegar até o diretório do projeto:

```bash
cd meu-projeto-react
```

### Passo 2: Instalação do Tailwind CSS

1. Instalar as dependências do Tailwind CSS:

```bash
npm install -D tailwindcss postcss autoprefixer
```

2. Criar o arquivo de configuração do Tailwind:

```bash
npx tailwindcss init -p
```

3. Atualizar o arquivo postcss.config.js:

```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

4. Criar um arquivo styles/tailwind.css e importar o Tailwind CSS:

```css
@import "tailwindcss/base";
@import "tailwindcss/components";
@import "tailwindcss/utilities";
```

5. Importar o arquivo tailwind.css no arquivo src/index.css:

```css
/_ src/index.css _/
import './styles/tailwind.css';
```

### Passo 3: Implementação do Arrastar e Soltar

1. Instalar a biblioteca "@hello-pangea/dnd":

```bash
npm install @hello-pangea/dnd
```

2. Atualizar o arquivo src/App.tsx com o código fornecido:

```tsx
// Arquivo: src/App.tsx
import { useState, FormEvent } from "react";
import { Task } from "./Task";
import { DragDropContext, Droppable } from "@hello-pangea/dnd";

function App() {
  const [newTask, setNewTask] = useState("");

  const [tasks, setTasks] = useState([
    {
      id: "0",
      name: "Estudar react com typescript",
    },
    {
      id: "1",
      name: "Estudar inglês",
    },
    {
      id: "2",
      name: "Pagar o aluguel",
    },
  ]);

  function handleAddTask(event: FormEvent) {
    event.preventDefault();

    if (newTask === "") return;

    const newItem = {
      id: `${tasks.length + 1}`,
      name: newTask,
    };
    setTasks((allTasks) => [...allTasks, newItem]);
    setNewTask("");
  }

  function reorder<T>(list: T[], startIndex: number, endIndex: number) {
    const result = Array.from(list);
    const [remove] = result.splice(startIndex, 1);
    result.splice(endIndex, 0, remove);

    return result;
  }

  function onDragEnd(result: any) {
    if (!result.destination) {
      return;
    }
    const items = reorder(tasks, result.source.index, result.destination.index);
    setTasks(items);
  }

  return (
    <div className="w-full h-screen flex bg-sky-950 flex-col items-center px-4 pt-52">
      <h1 className="font-bold text-4xl text-white mb-4">Tarefas</h1>

      <form className="w-full max-w-2xl mb-4 flex" onSubmit={handleAddTask}>
        <input
          type="text"
          placeholder="Digite o nome da tarefa..."
          className="flex-1 h-10 rounded-md px-2"
          value={newTask}
          onChange={(event) => setNewTask(event.target.value)}
        />
        <button
          type="submit"
          className="bg-blue-500 ml-4 rounded-md px-4 text-white font-medium"
        >
          Add
        </button>
      </form>

      <section className="bg-zinc-100 p-3 rounded-md w-full max-w-2xl">
        <DragDropContext onDragEnd={onDragEnd}>
          <Droppable droppableId="tasks" type="list" direction="vertical">
            {(provided) => (
              <article ref={provided.innerRef} {...provided.droppableProps}>
                {tasks.map((task, index) => (
                  <Task key={task.id} task={task} index={index} />
                ))}

                {provided.placeholder}
              </article>
            )}
          </Droppable>
        </DragDropContext>
      </section>
    </div>
  );
}

export default App;
```

### Passo 4: Criar o Componente de Tarefa

1.Criar um novo arquivo src/Task.tsx e adicionar o código fornecido:

```tsx
// Arquivo: src/Task.tsx
import { Draggable } from "@hello-pangea/dnd";

interface TaskProps {
  task: {
    id: string;
    name: string;
  };
  index: number;
}

export function Task({ task, index }: TaskProps) {
  return (
    <Draggable draggableId={task.id} index={index}>
      {(provided) => (
        <div
          {...provided.dragHandleProps}
          {...provided.draggableProps}
          ref={provided.innerRef}
          className="w-full bg-zinc-300 mb-2 last:mb-0 px-2 py-3 rounded border-[2px] border-zinc-400"
        >
          <p className="font-medium">{task.name}</p>
        </div>
      )}
    </Draggable>
  );
}
```

2. Importar o componente Task no arquivo src/App.tsx:

```tsx
// Arquivo: src/App.tsx (continuação)
import { Task } from "./Task";
// ... (código fornecido)
```

### Passo 5: Iniciar o Aplicativo

1. Executar o aplicativo:

```bash
npm run dev
```

2. Abrir o navegador e acessar http://localhost:3000.

### Conclusão

Você concluiu com sucesso a configuração de um projeto React usando Vite e Tailwind CSS, implementando a funcionalidade de arrastar e soltar com a biblioteca "@hello-pangea/dnd". Sinta-se à vontade para personalizar o projeto conforme suas necessidades e explorar mais recursos das bibliotecas utilizadas.
