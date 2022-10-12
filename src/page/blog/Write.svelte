<script>
	import { push } from 'svelte-spa-router';
	import { blogStore } from '../../store/blog';
	import {confirm, autoFocus } from '../../util/html';
	let newPost = {
		title: '',
		text: '',
	};
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
			blogStore.update((store) => ({
				...store,
				postList: [...store.postList, newPost],
			}));
			push('/blog');
		}
	};
</script>

<section>
	<h1>Post</h1>
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
