<script context="module">
	
	import client from '../sanityClient'
  export async function preload() {
		const filter = /* groq */`*[_type == "siteSettings"][0]`
		const projection = /* groq */`{
          ...,
          title,
          "image": image.asset->url,
          "alt": image.alt,
          "caption": image.caption,
      }`
      
      const query = filter + projection
      
      const siteInfo = await client
			.fetch(query)
			.catch((err) => this.error(500, err))
			
      return { siteInfo }
		}
</script>

<script>
	import {onMount} from 'svelte'
	import {fade, scale} from 'svelte/transition'
	// import Contact from './_contact.svelte'
	import SocialLinks from '../components/SocialLinks.svelte'
	import SEO from '../components/SEO.svelte'

	export let siteInfo
	const {title, image, alt} = siteInfo

	let show = false
	onMount(()=> show = true)
</script>

<style>
	section {
		position: relative;
		height: 100vh;
		width: 100%;
		display: grid;
		place-content: center;
		text-align: center;
		background-color: rgba(0,0,0,0.69);
		overflow: hidden;
	}
	
	img {
		position: absolute;
		top: 0;
		left: 0;
		object-fit: cover;
		width: 100%;
		height: 100%;
		z-index: -10;
	}

	h1 {
		font-size: 4rem;
		line-height: 1.1;
	}
</style>

<SEO {...siteInfo} description="A repository of work for Laila Wolf" />

<section>
	{#if show}
		<div class="card">

			<h1 id="{title}">{title}</h1>
			<SocialLinks/>
		</div>
			<img in:scale={{duration:2000, start: 1.2, opacity: 0.2}} src={image} {alt}>
	{/if}
</section>

<!-- <Contact /> -->

