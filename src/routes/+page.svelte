<svelte:head>
    <link rel="stylesheet" href="https://unpkg.com/@picocss/pico@latest/css/pico.min.css"/>
</svelte:head>

<script>
    let toDoList = [];

    let textInput = "";

    function addTodo() {
        if (textInput) {
            toDoList = [...toDoList, {content:  textInput, editing: false, checked: false}]
            textInput = "";
        }
        else
        {
            return;
        }
    }

    function setEditing(i, isEditing) {
        toDoList[i].editing = isEditing;
    }

    function deleteTodo(i) {
        toDoList.splice(i, 1);
        toDoList = toDoList;
    }
</script>

<div style="margin: 0 auto; width: 700px; box-sizing: border-box; padding: 20px; ">
    <h3 style="text-align: center; color: white; margin-top: 30px;">Miguel Ángel Manzano Méndez - 217814621</h3>
    <h4 style="text-align: center; color: white;">Programación para Internet - I5909 - D03</h4>
    <h1 style="text-align: center; color: white; margin-top: 100px; color: yellow;"> Tarea Libre: Lista de tareas con Svelte</h1>
    <h5 style="color: white;">¡Crea una tarea!</h5>
    <div style="display: flex">
        <input type="text" bind:value={textInput}/>
        <button style="width: 200px;" on:click={addTodo}>Agregar</button>
    </div>
    <h5 style="color: white; margin-top: 20px">Tareas agregadas</h5>
</div>

{#each toDoList as toDo, i}
<div style="display: flex; width: 700px; margin: 0 auto">
    {#if toDo.editing}
        <input type="text" bind:value={toDo.content}/>
    {:else}
        <input type="checkbox" bind:checked={toDo.checked} />
        {#if toDo.checked}
            <h4 style="flex-grow: 1; color: white; text-align: center; text-decoration: line-through; text-decoration-color: black;">{toDo.content}</h4>
        {:else}
            <h4 style="flex-grow: 1; color: white; text-align: center;">{toDo.content}</h4>
        {/if}
    {/if}
    <div style="display: flex"> 
        {#if toDo.editing}
            <button on:click={() => setEditing(i, false)}> Guardar</button>
        {:else}
            <button on:click={() => setEditing(i, true)}> Editar</button>
        {/if}
        <button on:click={() => deleteTodo(i)}> Eliminar</button>
    </div>
</div>
{/each}

<style>
    button{
        background-color: rgb(255, 187, 0);
        font-weight: 700;
        color: rgb(0, 0, 0);
        margin-left: 7px;
        border: solid 2px black;
    }
    input{
        color: white;
    }
</style>