# Todo App

Esta es una aplicación de lista de tareas (Todo App) construida en React. A continuación, explicaré detalladamente cada parte del código:

## Aprendizaje y uso de Skills Network

El desarrollo de esta aplicación Todo App en React implica varios conceptos y habilidades que se pueden adquirir a través de la plataforma Skills Network de IBM. A continuación, se describen los principales aspectos de aprendizaje y el uso de Skills Network:

### Aprendizaje de React

La aplicación Todo App está construida utilizando React, una popular biblioteca de JavaScript para construir interfaces de usuario. Para desarrollar esta aplicación, es necesario tener un conocimiento sólido de React, incluyendo los siguientes conceptos:

- Componentes funcionales y de clase
- Estado y ciclo de vida
- Hooks (useState, useEffect)
- Renderizado condicional
- Manejo de eventos
- Listas y keys
- Formularios controlados y no controlados

Skills Network ofrece diversos cursos y recursos para aprender React, como:

- **React.js Essentials**: Este curso introductorio cubre los conceptos básicos de React, incluyendo componentes, estado, props, eventos y ciclo de vida.
- **React Redux**: Este curso enseña cómo utilizar Redux, una biblioteca de gestión de estado, junto con React.
- **React Native Basics**: Este curso explica cómo construir aplicaciones móviles nativas utilizando React Native.

### Uso de Skills Network

Skills Network es una plataforma de aprendizaje en línea que ofrece una amplia variedad de cursos y recursos para adquirir habilidades en diferentes áreas, incluyendo desarrollo web, ciencia de datos, inteligencia artificial y más.

Al utilizar Skills Network para aprender React y construir la aplicación Todo App, se pueden aprovechar las siguientes características y beneficios:

1. **Contenido interactivo**: Los cursos en Skills Network incluyen videos, laboratorios prácticos, cuadernos de Jupyter y ejercicios interactivos que facilitan el aprendizaje.

2. **Badges y certificados**: Al completar cursos y proyectos, se obtienen badges y certificados que reconocen los conocimientos y habilidades adquiridos.

3. **Comunidad de aprendizaje**: Skills Network cuenta con una comunidad de estudiantes y instructores que pueden brindar apoyo, responder preguntas y compartir experiencias.

4. **Recursos adicionales**: Además de los cursos, Skills Network ofrece artículos, tutoriales y recursos complementarios para profundizar en temas específicos.

5. **Accesibilidad**: Los cursos y materiales de Skills Network están disponibles en línea, lo que permite un aprendizaje flexible y a tu propio ritmo.

Al combinar los conocimientos adquiridos en los cursos de React de Skills Network con la práctica de construir la aplicación Todo App, se consolidan las habilidades en el desarrollo de aplicaciones web modernas y se obtiene una experiencia práctica valiosa.

### Importaciones

```jsx
import React, { useState, useEffect } from "react";
import "./App.css";
```
Primero, se importan las dependencias necesarias de React y el archivo CSS para el estilo de la aplicación.

### Componente App
```jsx
const App = () => {
  // ...
}
```
Se define el componente funcional *App*, que contiene toda la lógica de la aplicación.

### Estado de la aplicación
```jsx
const [todos, setTodos] = useState([]);
const [todoEditing, setTodoEditing] = useState(null);
```
Se utilizan dos estados en la aplicación: todos para almacenar la lista de tareas y todoEditing para mantener el ID de la tarea que se está editando actualmente (si hay alguna).

### Cargar datos desde el almacenamiento local
```jsx
useEffect(() => {
  const json = localStorage.getItem("todos");
  const loadedTodos = JSON.parse(json);
  if (loadedTodos) {
    setTodos(loadedTodos);
  }
}, []);
```
Este efecto se ejecuta una sola vez cuando el componente se monta. Aquí, se obtienen los datos almacenados en el almacenamiento local (si existen) y se actualizan en el estado todos.

### Guardar datos en el almacenamiento local
```jsx
useEffect(() => {
  if (todos.length > 0) {
    const json = JSON.stringify(todos);
    localStorage.setItem("todos", json);
  }
}, [todos]);
```
Este efecto se ejecuta cada vez que el estado todos cambia. Aquí, se guardan los datos actualizados de todos en el almacenamiento local.

Funciones de manejo de tareas
### Agregar una nueva tarea
```jsx
function handleSubmit(e) {
  e.preventDefault();
  let todo = document.getElementById("todoAdd").value;
  const newTodo = {
    id: new Date().getTime(),
    text: todo.trim(),
    completed: false,
  };
  if (newTodo.text.length > 0) {
    setTodos([...todos].concat(newTodo));
  } else {
    alert("Enter Valid Task");
  }
  document.getElementById("todoAdd").value = "";
}
```
Esta función se ejecuta cuando se envía el formulario para agregar una nueva tarea. Crea un nuevo objeto newTodo con un id único, el texto de la tarea y un estado completed inicializado en false. Si el texto de la tarea no está vacío, se agrega a la lista de tareas usando el método concat. Luego, se limpia el campo de entrada.

### Eliminar una tarea
```jsx
function deleteTodo(id) {
  let updatedTodos = [...todos].filter((todo) => todo.id !== id);
  setTodos(updatedTodos);
}
```
Esta función se llama cuando se hace clic en el botón "Eliminar" de una tarea. Filtra la lista todos eliminando la tarea con el id proporcionado y actualiza el estado todos con la nueva lista.

### Marcar/Desmarcar una tarea como completada
```jsx
function toggleComplete(id) {
  let updatedTodos = [...todos].map((todo) => {
    if (todo.id === id) {
      todo.completed = !todo.completed;
    }
    return todo;
  });
  setTodos(updatedTodos);
}
```
Esta función se ejecuta cuando se hace clic en el checkbox de una tarea. Mapea la lista todos y cambia el estado completed de la tarea con el id proporcionado. Luego, actualiza el estado todos con la nueva lista.

### Editar una tarea
```jsx
function submitEdits(newtodo) {
  const updatedTodos = [...todos].map((todo) => {
    if (todo.id === newtodo.id) {
      todo.text = document.getElementById(newtodo.id).value;
    }
    return todo;
  });
  setTodos(updatedTodos);
  setTodoEditing(null);
}
```
Esta función se ejecuta cuando se hacen clic en el botón "Enviar ediciones" después de editar el texto de una tarea. Mapea la lista todos y actualiza el texto de la tarea con el id proporcionado con el nuevo valor ingresado en el campo de entrada. Luego, actualiza el estado todos con la nueva lista y establece todoEditing en null para salir del modo de edición.

### Renderizado de la aplicación
```jsx
return (
  <div id="todo-list">
    <h1>Todo List</h1>
    <form onSubmit={handleSubmit}>
      <input type="text" id="todoAdd" />
      <button type="submit">Add Todo</button>
    </form>
    {todos.map((todo) => (
      // ...
    ))}
  </div>
);
```
En la función de renderizado, se muestra el título de la aplicación y un formulario para agregar nuevas tareas. Luego, se mapea la lista todos y se renderiza cada tarea como un elemento div con su checkbox, texto y botones de acción (Editar y Eliminar).

### Exportación del componente
```jsx
export default App;
```
Finalmente, se exporta el componente App para que pueda ser importado y utilizado en otras partes de la aplicación.