<script>
	import Nav from '../components/Nav.svelte';

	export let segment;

</script>

<style>
	main {
		min-height: 100vh;
	}
	
	.layout {
		padding: calc(3rem + var(--headerHeight)) var(--containerPadding);
	}
</style>

<Nav {segment}/>

{#if !segment}
	<main>
		<slot></slot>
	</main>
{:else}
	 <main class="layout">
		 <slot></slot>
	 </main>
{/if}