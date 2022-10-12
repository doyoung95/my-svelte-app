<script>
	import Router from 'svelte-spa-router';
	import Todo from './page/Todo.svelte';
	import Home from './page/Home.svelte';
	import Blog from './page/blog/Blog.svelte';
	import Nav from './component/Nav.svelte';
	import Write from './page/blog/Write.svelte';
	import Detail from './page/blog/Detail.svelte';
	import Edit from './page/blog/Edit.svelte';

	const routes = {
		'/': Home,
		'/todo': Todo,
		'/blog': Blog,
		'/blog/write': Write,
		'/blog/:id': Detail,
		'/blog/edit/:id': Edit,
	};
</script>

<main>
	<Nav />
	<Router {routes} />
</main>

<style>
	main {
		width: 100vw;
	}
	:global(*) {
		padding: 0px;
		margin: 0px;
		box-sizing: border-box;
	}
	:global(section) {
		padding: 30px 60px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}
	:global(h1) {
		margin: 40px 0px;
	}
	:global(ul) {
		padding-inline-start: 0px;
	}
	:global(li) {
		list-style: none;
	}
</style>
