<script lang="ts">
	import { onMount } from 'svelte';
    import ts from 'typescript';

    let viewsize = 600;
    let viewshift = (viewsize-100)/2;
    let halfblob = viewshift/2;

	let blobs = new Array(80)
	.fill()
	.map((_, i) => {
		return {
			// Generates between 0-100 for initial X position.
			x: (Math.floor(Math.random() * viewsize)-viewshift),
			// Generates between 0-100 for initial Y position.
			y: Math.floor(Math.random() * viewsize)-viewshift,
			// Generates between __-__ for change in X position
			a: (Math.floor(Math.random() * 90) / 90),
			// Generates between __-__ for change in Y position
			b: (Math.floor(Math.random() * 90) / 90),
			// Generates interger between 35 - 150
			w: halfblob + Math.floor(Math.random() * halfblob),
			// Generates interger between 35 - 150
			h: halfblob + Math.floor(Math.random() * halfblob),
		};
	})

	onMount(() => {
		let frame: number;

		function loop() {
			frame = requestAnimationFrame(loop);

			blobs = blobs.map((splash) => {
			    splash.x += splash.a
				splash.y += splash.b
				if (splash.y > viewsize-viewshift) splash.y -= viewsize;
				if (splash.x > viewsize-viewshift) splash.x -= viewsize;
				return splash;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});
</script>

<div class="rainbow-container">
{#each blobs as b}
	<div
	   class="blobs"
		style="
		left: {b.x}vw;
		top: {b.y}vh;
		width: 0px;
		height: 0px;
		background-color: black;
		"
		>
		  <div
    		    class="blob"
    			style="
    			left: -{b.w*0.5}vw;
    			top: -{b.h*0.5}vh;
    			width: {b.w}vw;
    			height: {b.h}vw;
    			background-image: radial-gradient(hsla({Math.random() * 360}, 100%, 50%, 1), rgba(255,0,0,0) 70%);
                "
			>
			<p class="blob"
			style="
			    left: {b.w*0.5}vw;
    			top: {b.h*0.5}vh;
            ">

            </p>
			</div>
		<!-- background-image: radial-gradient(hsla({100, 100%, 50%, 1), rgba(255,0,0,0) 70%); -->
		<!-- {b.w} x {b.h} | {b.a} & {b.b} -->
		</div
	>
{/each}


<a href="/dance" class="text-decoration-none text-white">
    <div class="position-absolute top-50 start-50 translate-middle">
        <span class="border border-white border-5 rounded-5 text-center py-3 px-5 text-white ">
        Fox & Owl
        </span>
    </div>
    </a>

</div>

<style>
    .rainbow-container {
        height: 100vh;
        width: 100vw;
        left: 0px;
        top: 0px;
        position: absolute;
        overflow: hidden;
        z-index: 0;
        background-color: hsla(50, 100%, 50%, 1);
    }
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
