<!-- <script>
	let { text, todos, todo, idx } = $props();

	let isFocus = $state(false);

	function remove(idx) {
		todos = todos.filter((item, index) => index !== idx);
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
</script>

<div
	onclick={() => (isFocus === false ? (isFocus = idx) : (isFocus = false))}
	class="border flex p-4 rounded-2xl border-gray-600 w-full justify-between items-center {isFocus ===
		idx && 'ring ring-gray-200 ring-offset-4 ring-offset-black'}"
>
	<input
		on:input={() => check(idx)}
		type="checkbox"
		checked={todo.done}
		class="w-6 h-6 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-600 focus:ring-2"
	/>
	<input
		bind:value={todo.text}
		on:keypress={(e) => e.key === 'Enter' && edit(idx)}
		value={todo.text}
		class=" outline-none bg-gray-500 p-4 {todo.done ? 'line-through' : ''}"
	/>

	<button
		class="text-xl font-extrabold active:border-2 active:border-gray-200 w-8 p-1 rounded rounded-full"
		on:click={() => remove(idx)}>X</button
	>
</div> -->
