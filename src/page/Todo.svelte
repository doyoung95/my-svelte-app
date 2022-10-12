<script>
	import { todoStore } from '../store/todo';
	import { autoFocus } from '../util/html';
	let todoList;
	todoStore.subscribe((store) => {
		todoList = store.todoList;
	});

	let newTodo = '';
	const completeStyle = 'background: black;';

	const onClickTodo = (idx) => {
		const tempTodoList = [...todoList];
		tempTodoList[idx].isComplete = !tempTodoList[idx].isComplete;

		todoStore.update((store) => ({
			...store,
			todoList: tempTodoList,
		}));
	};

	const onInputNewTodo = (e) => {
		const { value } = e.target;
		newTodo = value;
	};

	const onKeydownNewTodo = (e) => {
		const { keyCode } = e;
		if (keyCode !== 13) {
			return;
		}
		const tempTodoList = [
			...todoList,
			{
				text: newTodo,
				isComplete: false,
			},
		];
		todoStore.update((store) => ({
			...store,
			todoList: tempTodoList,
		}));
		newTodo = '';
	};
	const onClickDelete = (idx) => {
		todoList = todoList.filter((_, _idx) => idx !== _idx);
	};
</script>

<section>
	<h1>Svelte Todo List</h1>
	<ul class="todoList">
		{#each todoList as todo, idx}
			<li class="todo">
				<div class="toggle" on:click={() => onClickTodo(idx)}>
					<div
						style={`
						margin-right: 10px;
						width: 20px;
						height: 20px;
						border: 1px solid black;
						${todo.isComplete ? completeStyle : ''}
						`}
					/>
					<p>{todo.text}</p>
				</div>
				<span on:click={() => onClickDelete(idx)}>Delete</span>
			</li>
		{/each}
	</ul>
	<input
		value={newTodo}
		placeholder="New todo"
		on:input={onInputNewTodo}
		on:keydown={onKeydownNewTodo}
		use:autoFocus
	/>
</section>

<style>
	.todoList {
		display: flex;
		flex-direction: column;
		width: 400px;
		gap: 10px;
	}
	.todo {
		padding: 0px 5px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		border-radius: 8px;
	}
	.todo:hover {
		background: #eee;
	}
	.toggle {
		cursor: pointer;
		display: flex;
		align-items: center;
	}
	span {
		cursor: pointer;
		font-size: 12px;
		color: red;
	}
	input {
		margin-top: 20px;
		width: 400px;
		height: 30px;
	}
</style>
