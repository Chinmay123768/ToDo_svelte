<script>
      let todos = [];
	  let task = "";
	  let filter = 'all';
	  function addTask (){
		  todos = [{
			  task: task,
              status: "pending",
		  }, ...todos];
		  task ="";
	  }
	  function markComplete(i){
          todos[i].status = 'completed';
		  todos = [...todos];
	  }
	  function removeTask(i){
          todos.splice(i,1);
		  todos = [...todos];
	  }
</script>
<body>
	
<div class="header">MY TODO LIST</div>
<div class="container">
	
	<div class="todo">
		<div class="form">
			<input type="text" bind:value={task}/>
			<button on:click={addTask}>
				Add
			</button>
		</div>
		<div class="tasks">
			{#each todos as todo, i}
				{#if filter == "all"}
				<div class="task">
					<div>{todo.task}</div>
					<button class="{todo.status == 'completed'?'active':''}" id="tick"  on:click="{()=>{markComplete(i)}}">&#10004</button>
					<button id="wrong" on:click="{()=>{removeTask(i)}}">&#10006</button>
				</div>
				{:else if filter == "completed"}
				{#if todo.status == "completed"}
				<div class="task">
					<div>{todo.task}</div>
					
					<button id="wrong" on:click="{()=>{removeTask(i)}}">&#10006</button>
				</div>
				{/if}
				{:else}	
				{#if todo.status == 'pending'}
				<div>{todo.task}</div>
					<button class="{todo.status == 'completed'?'active':''}" id="tick"  on:click="{()=>{markComplete(i)}}">&#10004</button>
					
				{/if}
				{/if}
		{/each}
			

		</div>
		<div class="filters">
			<button class="{filter == 'all'? 'active': ''}" on:click="{()=>{filter = 'all'}}">All</button>
			<button class="{filter == 'completed'? 'active': ''}" on:click="{()=>{filter = 'completed'}}">Completed</button>
			<button  class = "{filter == 'incomplete'? 'active': ''}" on:click="{()=>{filter = 'incomplete'}}">Incomplete</button>

		</div>
	</div>

</div>
</body>
<style>
      .container{
		  width: 100%;
		  height: 100vh;
		  display: flex;
		  justify-content: center;
		  align-items: center;
		  padding: 8px;
		  background-color: rosybrown;
    }
	.todo{
		padding: 15px;
		border-radius: 10px;
		width: 500px;
		background-color: whitesmoke;
	}
	.todo .form{
		display: flex; 
		padding: 8px;
	}
	button, input{
      border:2px solid black ;
	  box-shadow: 3px solid black;
	  cursor: pointer;
	}
	.todo .form button{
          margin-left: 5px;
		  border-radius: 10px;
		  width: 50px;
		  background-color: darkcyan;
		  color:whitesmoke;
	}
	.filters button{
		border-radius: 10px;
		
		text-align: center;
		font-family: Verdana, Geneva, Tahoma, sans-serif;
	}
	#tick{
		color: green;
        margin-right: 2px;
	}
	#wrong{
		color: red;
	}
	.todo .tasks > .task{
		display: flex;
		
		margin: 10px 0px;
	}
	.todo .tasks {
		min-height: 200px;
	}
	.todo .tasks > .task > button {
		width: 30px;
		height: 30px;
		padding: 2px;
		
		border-radius: 50%;
		align-items: center;
	}
	.todo .tasks > .task > div{
		flex: 1;
	}
	.todo .filters {
		display: flex;
		
	}
	.todo .filters > button{
		margin: 10px;
		padding: 8px 6px;
		border: 1px solid rgb(15, 15, 92);
		border-radius: 20px;
		display: flex;
	}
	.header{
		text-align: center;
		font-size: larger;
		font-weight: bolder;
		font-family: cursive;
		color: darkgreen;
	}
	.todo .filters > button.active{
          background-color: firebrick;

	}
	.todo .tasks > .task >button.active{
		background-color: orange;
	}
</style>