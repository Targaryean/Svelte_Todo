<svelte:head>
    <link rel="stylesheet" href="https://unpkg.com/@picocss/pico@latest/css/pico.min.css">
</svelte:head>

<script>
      import "../app.css";
    let toDoList = []; // array of ToDos
    let textInput = "";

    function addToDo() {
        toDoList = [...toDoList, { content: textInput, editing: false, checked: false }]
        textInput = ""; //clearing the input field
    }

    function setEditing(i, isEditing) {
        toDoList[i].editing = isEditing; // true / false
    }


    function deleteTodo(i) {
        toDoList.splice(i, 1);
        toDoList = toDoList; // https://svelte.dev/tutorial/updating-arrays-and-objects
    }
</script>



<div class="container mx-auto p-4 rounded-lg text-white shadow-md">
    <h2 class="text-center text-2xl font-bold mb-4">ToDo List</h2>
    <div class=" p-2 flex items-center mb-4">
      <input
        type="text"
        bind:value={textInput}
        class="w-full bg-gray-800 border border-gray-700 rounded-md px-8 py-1 focus:outline-none focus:ring-blue-500 focus:ring-2"
      >
      <button
        class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded shadow-md "
        on:click={addToDo}
      >
        Add
      </button>
    </div>
  
    {#each toDoList as toDo, i}
      <div class="gap-1 flex items-center justify-between mb-2 p-2 ">
        {#if toDo.editing}
          <input
            type="text"
            bind:value={toDo.content}
            class="w-full bg-gray-800 border border-gray-700 rounded-md px-3 py-2 focus:outline-none focus:ring-blue-500 focus:ring-2"
          >
        {:else}
          <input
            type="checkbox"
            bind:checked={toDo.checked}
            class="mr-2 w-4 h-4 accent-blue-500 focus:ring-blue-500 focus:ring-2"
          >
          <h4 class="text-xl font-medium break-words">{toDo.content}</h4>
        {/if}
        <div class="flex items-center">
          {#if toDo.editing}
            <button
              class="mr-2 bg-green-500 hover:bg-green-700 text-white font-bold px-2 py-1 rounded shadow-md"
              on:click={() => setEditing(i, false)}
            >
              Save
            </button>
          {:else}
            <button
              class="mr-2 bg-teal-500 hover:bg-teal-700 text-white font-bold px-2 py-1 rounded shadow-md"
              on:click={() => setEditing(i, true)}
            >
              Edit
            </button>
          {/if}
          <button
            class="bg-red-500 hover:bg-red-700 text-white font-bold px-2 py-1 rounded shadow-md"
            on:click={() => deleteTodo(i)}
          >
            Delete
          </button>
        </div>
      </div>
    {/each}
  </div>
