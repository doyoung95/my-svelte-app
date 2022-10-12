<script>
	import { push } from 'svelte-spa-router';
	import { blogStore } from '../../store/blog';
	let postList;
	blogStore.subscribe((store) => {
		postList = store.postList;
	});
	const onClickWriteButton = () => {
		push('/blog/write');
	};
	const onClickPost = (idx) => {
		push(`/blog/${idx}`);
	};
</script>

<section>
	<h1>Your post list</h1>
	{#if !postList.length}
		<pre>Empty...</pre>
	{:else}
		<ul>
			{#each postList as post, idx}
				<li on:click={() => onClickPost(idx)}>
					{idx + 1}. {post.title}
				</li>
			{/each}
		</ul>
	{/if}
	<button on:click={onClickWriteButton}>Write new post</button>
</section>

<style>
	button {
		margin-top: 30px;
	}
	li {
		cursor: pointer;
	}
</style>
