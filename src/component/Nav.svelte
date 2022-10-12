<script lang="typescript">
	import { push } from 'svelte-spa-router';
	import { pageList } from '../util/page';

	const onClickPage = (route) => {
		push(route);
	};
</script>

<ul>
	{#each pageList as page, idx}
		<li on:click={() => onClickPage(page.route)}>{page.title}</li>
	{/each}
</ul>

<style>
	ul {
		display: flex;
	}

	li {
		cursor: pointer;
		list-style: none;
		font-size: 16px;
		font-weight: 700;
		margin-right: 12px;
	}
</style>
