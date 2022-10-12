<script>
	import { blogStore } from '../../store/blog';
	import { push } from 'svelte-spa-router';
	export let params = { id: 0 };
	let postDetail;
	blogStore.subscribe((store) => {
		postDetail = store.postList[params.id];
	});
	const onClickEdit = () => {
		push(`/blog/edit/${params.id}`);
	};
</script>

<section>
	<div>
		<h1>{postDetail.title}</h1>
		<p class="editButton" on:click={onClickEdit}>Edit</p>
	</div>
	<textarea readonly>{postDetail.text}</textarea>
</section>

<style>
	div {
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		width: 100%;
	}
	.editButton {
		position: absolute;
		top: 50%;
		right: 0px;
		transform: translateY(-50%);
		cursor: pointer;
		align-self: flex-end;
		color: blue;
	}
	textarea {
		resize: none;
		padding: 10px;
		width: 100%;
		border: 0px;
	}
</style>
