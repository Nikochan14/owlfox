<script lang="ts">
	import { onMount } from 'svelte';
    import ts from 'typescript';

	let blobs = new Array(200)
	.fill()
	.map((_, i) => {
		return {
			// Generates between 0-100
			x: Math.random() * 150,
			// Generates between 0-100
			y: 0 - Math.random() * 150,
			// Generates interger between 20-50
			w: 20 + Math.floor(Math.random() * 11) * 3,
			// Generates between 1-3 (with 1 decimal place)
			m: (10 + Math.floor(Math.random() * 20)) / 10,
			// Generates between 0-360
			c: Math.floor(Math.random() * 360)
		};
	})

	onMount(() => {
		let frame: number;

		function loop() {
			frame = requestAnimationFrame(loop);

			blobs = blobs.map((splash) => {
			    splash.x += 8
				splash.y += 8
				if (splash.y > 120) splash.y = -20;
				if (splash.x > 120) splash.x = -20;
				return splash;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

{#each blobs as b}
	<div
	   class="blobs"
		style="
		left: {b.x}%;
		top: {b.y}%;
		width: 0px;
		height: 0px;
		overflow: visible;
		background-color: blue;
		"
		>
		  <div
    		    class="blob"
    			style="
    			left: -{b.w * 0.5}vw;
    			top: -{b.w * b.m * 0.5}vh;
    			width: {b.w}vw;
    			height: {b.w * b.m}vh;
    			background-image: radial-gradient(hsla({Math.random() * 360}, 100%, 50%, 1), rgba(255,0,0,0) 70%);
    			"
			>
			</div>
		<!-- background-image: radial-gradient(hsla({100, 100%, 50%, 1), rgba(255,0,0,0) 70%); -->
		</div
	>
{/each}

<div class="position-absolute top-50 start-50 translate-middle">
    <span class="border border-white border-5 rounded-5 text-center py-3 px-5 text-white ">
      EVERYBODY DANCE NOW
    </span>
</div>

<style>
	.blobs {
		position: absolute;
		font-size: 5vw;
		user-select: none;
		font-size: 1em;
		scale: 100%;
	}
	.blob {
	   position: relative;
	}
</style>
