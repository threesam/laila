<script context="module">
	
	import client from '../../sanityClient'
  export async function preload() {
		const filter = /* groq */`*[_type == "author"][0]`
		const projection = /* groq */`{
          ...,
          name,
          "image": mainImage.asset->url,
          "alt": mainImage.alt,
          "caption": mainImage.caption,
      }`
      
      const query = filter + projection
      
      const author = await client
			.fetch(query)
			.catch((err) => this.error(500, err))
			
      return { author }
		}
</script>

<script>
	import BlockContent from '@movingbrands/svelte-portable-text'
	import serializers from '../../components/serializers'
	import SEO from '../../components/SEO.svelte'

	export let author
	const { name, image, alt, caption, bio} = author
</script>

<style>
	img {
		filter: grayscale(100%);
	}
</style>

<SEO title="About Laila" description="Information about and links to the life and work of Laila Wolf" {image} {alt} />

<h1>About Laila</h1>

<img src={image} {alt}>

<BlockContent blocks={bio} {serializers} />