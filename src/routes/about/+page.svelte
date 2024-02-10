<script lang="ts">

</script>

<svelte:head>
	<title>chengcpu ~/About</title>
</svelte:head>

<div class="content">
	<h2>About</h2>
    <p>
			My name is Cheng, you can also call me Lee.
			I like <span class="text-rose">programming</span>, <span class="text-rose">computer science</span> and <span class="text-rose">solving completely impractical, difficult problems</span>
    </p>
    <p>
			Owner and maintainer of <a href="https://visamap.co/" rel="me" class="u-url">visa-map</a>
    </p>
    <hr />
    <h3 id="contact">Contact</h3>
		<p>@ -> <a href="mailto:ChengCPU@proton.me?subject=Hello!" class="u-email">ChengCPU@proton.me</a></p>
</div>

<style lang="sass">
	ul
		padding-top: 0.15rem
		margin: 0

	li
		padding-left: 0.5rem
		padding-top: 0.25rem
		vertical-align: middle

	h3
		scroll-margin-top: 5.5rem

	.muted
		color: var(--color-muted) !important

	details
		margin: 0
		padding-top: 0.5rem

	details > summary
		cursor: pointer

	#discordAvatar
		border-radius: 50%
		height: 2em
		vertical-align: middle

	.copy
		user-select: all

	.click
		cursor: pointer
</style>
