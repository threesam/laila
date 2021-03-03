<script>
	export let segment;
</script>

<header>

	<nav>
		<a aria-current="{segment === undefined ? 'page' : undefined}" href=".">home</a>
		<a aria-current="{segment === 'about' ? 'page' : undefined}" href="about">about</a>
		<!-- <a rel="prefetch" aria-current="{segment === 'blog' ? 'page' : undefined}" href="blog">blog</a> -->
	</nav>
		
</header>