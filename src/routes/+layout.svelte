<script lang="ts">
	import "../app.sass";
	import { afterNavigate, beforeNavigate } from "$app/navigation";
	import { browser } from "$app/environment";
	import { navigating, page } from "$app/stores";
	import { onMount } from "svelte";

	let navprogress = 30;
	let navInterval: number;
	let showProgress = false;

	export let timeDisplay: string = new Date().toLocaleString();
	setInterval(() => {
		timeDisplay = new Date().toLocaleString();
	}, 500);

	beforeNavigate(() => {
		navprogress = 5;
		showProgress = true;
		navInterval = setInterval(() => {
			navprogress += navprogress <= 90 ? 2.5 : navprogress < 95 ? 0.1 : 0;
		}, 500);
	});

	onMount(() => {
		setInterval(() => {
			if(!navigating) {
				if(showProgress) resetProgress();
			}
		}, 2000);
	})

	function resetProgress() {
		clearInterval(navInterval);
		navprogress = 100;

		setTimeout(() => {
			showProgress = false;
		}, 300);

		setTimeout(() => {
			navprogress = 0;
		}, 500);
	}

	afterNavigate(resetProgress);
</script>

<div id="loadingBar" style:width={`${navprogress}%`} class:active={showProgress} />

<nav class="sticky">
	<div>
		<div id="header">
			<p id="site-name">chengcpu<sup>★</sup></p>
			<p id="time-display">
				{#if !browser}<abbr title="Rendered at">r=</abbr>{/if}{timeDisplay}
			</p>
		</div>
		<div id="nav">
			<a href="/" class:current={$page.url.pathname == "/"}>~/Home</a>
			<!-- <a href="/projects" class:current={$page.url.pathname == "/projects"}>~/Projects</a> -->
			<a href="/about" class:current={$page.url.pathname == "/about"}>~/About</a>
		</div>
		<hr />
	</div>
</nav>

<div>
	<slot />
</div>

<hr />
<div id="footer">
	<p>🇬🇧 🏴󠁧󠁢󠁥󠁮󠁧󠁿 🇪🇸 🇧🇷 🇭🇰</p>
	<p>
		The source code of this site can be viewed
		<a href="//github.com/ChengCPU/chengpu.github.io">here</a>
	</p>

	<noscript>
		<div id="nojs">
			<p>JavaScript is currently not enabled or not supported, though this site should still work fine.</p>
			<p>If there are any accessibility issues, please do not hesitate to contact me.</p>
			<p>
				You can find methods to contact me on
				{#if $page.url.pathname == "/about"}
					this exact page.
				{:else}
					the <a href="/about">about</a> page.
				{/if}
			</p>
		</div>
	</noscript>

</div>

<style lang="sass">
	#header
		display: flex
		justify-content: space-between

		p
			margin: 0.75em 0.75em

	#time-display
		color: #5BCEFA

	#site-name
		color: #F5A9B8

	@media (prefers-color-scheme: light)
		#time-display
			color: #49A7CC

		#site-name
			color: #CC7E97

	#nav
		display: flex
		justify-content: start
		margin: 0 1rem

		a
			margin: 0 0.35rem

	.current
		color: var(--color-rose)

	#loadingBar
		position: fixed
		top: 0
		left: 0
		height: 0
		background-color: var(--color-love)
		transition-property: width, height
		transition-duration: 150ms
		z-index: 1

		&.active
			height: 0.2rem

	#footer
		margin: 0 1rem
		padding-bottom: 2rem

		p
			margin-top: 0.25rem
			margin-bottom: 0

	.webring
		padding: 0.2rem 0.5rem
		border-width: 2px
		border-radius: 30px
		border-style: solid
		border-color: var(--hl-med)

	#nojs
		margin: 0
		padding-top: 1em
		color: var(--color-pine)
		text-align: center
		p
			margin: 0

	nav
		background-color: var(--color-base)

	.sticky
		position: sticky
		top: 0
</style>