<main class="app">
	<InputForm on:addTodo={addNewTodo} />
	<div class="inner">
		<Filter activeFilter={filter} on:filter={applyFilter} />
		<Status {total} {complete} />
		<ToDoList
			todoList={filteredList()}
			on:checked={checkTodo}
			on:edit={editTodo}
			on:delete	={deleteTodo}
		/>
		<Actions
			on:removeComplete={removeCompelte}
			on:checkAll={checkAll}
		/>
	</div>
</main>

<script>
	import InputForm from './components/InputForm.svelte';
	import Filter from './components/Filter.svelte';
	import Status from './components/Status.svelte';
	import ToDoList from './components/ToDoList.svelte';
	import Actions from './components/Actions.svelte';

	let todoList = [
		{ id: 0, title: 'Get back to Vladimir', complete: false },
		{ id: 1, title: 'Return to Moscow from Kazan', complete: true },
	];
	let filter = 'ALL';

	function addNewTodo({ detail }) {
		const lastTodoId = todoList.length ? todoList[todoList.length - 1].id : -1;
		todoList = [...todoList, {
			id: lastTodoId + 1,
			title: detail,
			complete: false
		}];
	}

	function checkTodo({ detail: { index, checked} }) {
		todoList[index].complete = checked;
	}

	function editTodo({ detail: { index, value } }) {
		todoList[index].title = value;
	}

	function deleteTodo({ detail: index }) {
		todoList = todoList.filter((_, idx) => idx !== index);
	}

	function removeCompelte() {
		todoList = todoList.filter(todo => !todo.complete);
	}

	function checkAll() {
		todoList = todoList.map(todo => ({
			...todo,
			complete: true
		}));
	}

	function applyFilter({ detail }) {
		filter = detail;
	}

	$: total = todoList.length;
	$: complete = todoList.filter(todo => todo.complete).length;
	$: filteredList = () => {
		switch (filter) {
			case 'ALL':
				return todoList;
			case 'ACTIVE':
				return todoList.filter(todo => !todo.complete);
			case 'COMPLETED':
				return todoList.filter(todo => todo.complete);
			default:
				return todoList;
		}
	}
</script>

<style>
	.app {
		max-width: 620px;
		margin: 30px auto;
		padding: 0 10px;
	}

	.inner {
		margin-left: 50px;
		margin-right: 50px;
	}
	@media screen and (max-width: 600px) {
		.inner {
			margin: 0;
		}
	}
</style>