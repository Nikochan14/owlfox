<script lang="ts">
	import { onMount } from 'svelte';
    import ts from 'typescript';

	let blobs = new Array(40)
	.fill()
	.map((_, i) => {
		return {
			// Generates between 0-100
			x: 25 - Math.random() * 150,
			// Generates between 0-100
			y: 75 - Math.random() * 250,
			// Generates interger between 20-100
			w: 35 + Math.floor(Math.random() * 116),
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
			    splash.x += 3
				splash.y += 3
				if (splash.y > 175) splash.y = -75;
				if (splash.x > 125) splash.x = -25;
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
		left: {b.x}vw;
		top: {b.y}vh;
		width: 0px;
		height: 0px;
		overflow: visible;
		background-color: black;
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
			<p class="blob"
			style="
			    left: {b.w * 0.5}vw;
    			top: {b.w * b.m * 0.5}vh;
            ">
            {b.w}, {b.w*b.m} & {b.m}
            </p>
			</div>
		<!-- background-image: radial-gradient(hsla({100, 100%, 50%, 1), rgba(255,0,0,0) 70%); -->
		</div
	>
{/each}

<div class="position-absolute top-50 start-50 translate-middle">
    <span class="border border-white border-5 rounded-5 text-center py-3 px-5 text-white ">
      Fox & Owl
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
