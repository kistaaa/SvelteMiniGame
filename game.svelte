<script>
	const mapWidth = 8;
	const mapHeight = 8;
	let position = {x: mapWidth/2, y: mapHeight/2}
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
				map[x][y] = Math.round(Math.random() * 10) /10
			}
		}
	}
	
	makeMap();
	scroll();

</script>

<style>
	:global(body) {margin:0; padding:0; overflow:hidden}
	#controls button{position:fixed; width:64px; height:64px; font-size:24px; margin-bottom:0}
	#up{top:0; left:50%; margin-left:-32px; border-bottom-left-radius:64px; border-bottom-right-radius:64px}
	#down{bottom:0; left:50%; margin-left:-32px; border-top-left-radius:64px; border-top-right-radius:64px}
	#left{left:0; top:50%; margin-top:-32px; border-top-right-radius:64px; border-bottom-right-radius:64px}
	#right{right:0; top:50%; margin-top:-32px; border-top-left-radius:64px; border-bottom-left-radius:64px}
	.row {display:flex;}
	.cell {flex-shrink:0;width:100vw; height:100vh; line-height:100vh; text-align:center; font-size:42px; font-weight:bold;}
	.map{width:100vw; height:100vh;}
</style>


<div class="map"> 
{#each map as y, iy}
	<div class="row">
		{#each y as x, ix}
				<div class="cell">
					{ix},{iy} - {position.x},{position.y}
				</div>
		{/each}
	</div>
{/each}
</div>

<div id="controls">
	<button id="up" on:click={moveUp}>🡱</button>
	<button id="down" on:click={moveDown}>🡳</button>
	<button id="left" on:click={moveLeft}>🡰</button>
	<button id="right" on:click={moveRight}>🡲</button>
</div>
