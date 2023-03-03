<script>
	import { onMount } from 'svelte';
	const mapWidth = 7;
	const mapHeight = 7;
	let position = {x: 0, y: Math.floor(mapHeight/2)}
	let map = []
	
	  function scroll() {
			window.scrollTo({
				top: position.y * window.innerHeight,
				left: position.x * window.innerWidth,
				behavior: 'smooth'
			});
  	}
	
	function moveUp() {
		position.y -= 1;
		if(position.y < 0) position.y = 0;
		position = position;
		scroll();
	}
	function moveDown(){
		position.y += 1;
		if(position.y > mapHeight) position.y = mapHeight;
		position = position;
		scroll();
	}
	function moveLeft(){
		position.x -= 1;
		if(position.x < 0) position.x = 0;
		position = position;
		scroll();
	}
	function moveRight(){
		position.x += 1;
		if(position.x > mapWidth) position.x = mapWidth;
		position = position;
		scroll();
	}
	
	function makeMap(){
		for(let x=0; x<=mapWidth; x++) {
			map[x] = []
			for(let y=0; y<=mapHeight; y++) {
				map[x][y] = {enemies: !!Math.round(Math.random()), items: !!Math.round(Math.random())}
			}
		}
	}
	
	makeMap();
	
	onMount(() => {
		scroll();
	});
	

</script>

<style>
	:global(body) {margin:0; padding:0; overflow:hidden}
	#controls button{position:fixed; font-size:30px; margin-bottom:0; background:#fff;  padding:0; border:2px solid #999; cursor:pointer}
	.vbut{width:64px; height:100px;}
	.hbut{width:100px; height:64px;}
	#up{top:0; left:50%; margin-left:-50px; border-bottom-left-radius:46px; border-bottom-right-radius:46px}
	#down{bottom:0; left:50%; margin-left:-50px; border-top-left-radius:46px; border-top-right-radius:46px}
	#left{left:0; top:50%; margin-top:-50px; border-top-right-radius:46px; border-bottom-right-radius:46px}
	#right{right:0; top:50%; margin-top:-50px; border-top-left-radius:46px; border-bottom-left-radius:46px}
	.row {display:flex;}
	.cell {flex-shrink:0;width:100vw; height:100vh; line-height:100vh; text-align:center; font-size:42px; font-weight:bold; border:2px solid #999; box-sizing:border-box;}
	.map{width:100vw; height:100vh;}
</style>


<div class="map"> 
{#each map as y, iy}
	<div class="row">
		{#each y as x, ix}
				<div class="cell">
					{ix},{iy} - enemies: {x.enemies} - items: {x.items}
				</div>
		{/each}
	</div>
{/each}
</div>

<div id="controls">
	{#if position.y > 0}
		<button class="hbut" id="up" on:click={moveUp}>🡱</button>
	{/if}
	{#if position.y < mapHeight}
		<button class="hbut" id="down" on:click={moveDown}>🡳</button>
	{/if}
	{#if position.x > 0}
		<button class="vbut" id="left" on:click={moveLeft}>🡰</button>
	{/if}
	{#if position.x < mapWidth}
		<button class="vbut" id="right" on:click={moveRight}>🡲</button>
	{/if}
</div>
