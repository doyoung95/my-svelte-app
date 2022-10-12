<script>
	import { get } from 'svelte/store';
	import { push } from 'svelte-spa-router';
	import { blogStore } from '../../store/blog';
	import { confirm, autoFocus } from '../../util/html';
	export let params = { id: undefined };
	let newPost = { ...get(blogStore).postList[params.id] };

	const onInput = (e) => {
		const { value, name } = e.target;
		newPost = { ...newPost, [name]: value };
	};
	const onClickCancel = () => {
		if (confirm()) {
			push('/blog');
		}
	};

	const onClickConfirm = () => {
		const { title, text } = newPost;
		if (!title || !text) {
			return window.alert('Title or text can not be empty.');
		}
		if (confirm()) {
			blogStore.update((store) => {
				const editPostList = [...store.postList];
				editPostList[params.id] = newPost;
				return {
					...store,
					postList: editPostList,
				};
			});
			push('/blog');
		}
	};
</script>

<section>
	<h1>Edit</h1>
	<input
		name="title"
		placeholder="title"
		bind:value={newPost.title}
		on:input={onInput}
		use:autoFocus
	/>
	<textarea
		name="text"
		placeholder="text"
		value={newPost.text}
		on:input={onInput}
	/>
	<div class="buttonWrap">
		<button on:click={onClickCancel}>cancel</button>
		<button on:click={onClickConfirm}>confirm</button>
	</div>
</section>

<style>
	input {
		padding: 0px 10px;
		width: 100%;
		height: 40px;
	}
	textarea {
		resize: none;
		padding: 10px;
		width: 100%;
		height: 600px;
		border: 1px solid black;
	}
	.buttonWrap {
		display: flex;
		justify-content: space-around;
		width: 100%;
		height: 100px;
	}
	button {
		width: 200px;
		height: 100%;
	}
</style>
