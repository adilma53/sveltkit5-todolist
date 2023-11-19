<script>
	let text = $state('');
	let todos = $state([]);

	let isFocus = $state(false);

	function remove(idx) {
		todos = todos.filter((item, index) => index !== idx);
	}

	function add() {
		const obj = {};
		obj['text'] = text;
		obj['done'] = false;
		todos = [...todos, obj];

		text = '';
	}

	function check(idx) {
		let temp = todos;
		temp[idx] = { ...temp[idx], done: !temp[idx]['done'] };
		todos = temp;
	}

	function edit(idx) {
		let temp = todos;
		temp[idx] = { ...temp[idx], text: temp[idx]['text'] };
		todos = temp;
	}

	$effect(() => {
		const storagTodos = localStorage.getItem('todos');
		storagTodos && (todos = JSON.parse(storagTodos));
	});

	$effect(() => {
		localStorage.setItem('todos', JSON.stringify(todos));
	});
</script>

<div
	class="bg-black text-xl font-mono text-gray-200 flex flex-col justify-center items-center min-h-screen"
>
	<input
		placeholder="Add Todo"
		onkeypress={(e) => e.key === 'Enter' && add()}
		bind:value={text}
		class="transition outline-none focus:ring focus:ring-gray-200 focus:ring-offset-4 focus:ring-offset-black bg-black text-white p-3 rounded-2xl my-5 w-1/3"
	/>

	<ul class="space-y-3 flex flex-col w-1/3">
		{#each todos as todo, idx}
			<li
				onclick={() => (isFocus === false ? (isFocus = idx) : (isFocus = false))}
				class="transition flex p-4 rounded-2xl border-gray-600 w-full justify-between items-center {isFocus ===
					idx && 'ring ring-gray-200 ring-offset-4 ring-offset-black'}"
			>
				<input
					on:input={() => check(idx)}
					type="checkbox"
					checked={todo.done}
					class="transition w-6 h-6 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-600 focus:ring-2"
				/>
				<input
					bind:value={todo.text}
					on:keypress={(e) => e.key === 'Enter' && edit(idx)}
					value={todo.text}
					class="mx-7 grow transition outline-none bg-black p-4 {todo.done ? 'line-through' : ''}"
				/>

				<button
					class="transition text-xl font-extrabold active:border-2 active:border-gray-200 w-8 p-1 rounded rounded-full"
					on:click={() => remove(idx)}>X</button
				>
			</li>
		{/each}
	</ul>
</div>

<svelte:head>
	<link rel="stylesheet" href="https://unpkg.com/tailwindcss@2.2.19/dist/tailwind.min.css" />
</svelte:head>
