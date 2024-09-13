<script>
	import Tile from "./Tile.svelte";

</script>
<div id="tiles">
	<div id="leftTiles">
		<slot name="uvIndex"></slot>
		<slot name="wind"></slot>
	</div>
	<div id="rightTiles">
		<slot name="sunset"></slot>
		<slot name="precipitation"></slot>
	</div>
</div>

<style>
    	.innerTile {
		width: 125px;
		height: 125px;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-direction: column;
	}
    .tile {
		margin-bottom: 5px;
		margin-right: 5px;
		flex: 50%;
		width: 135px;
		height: 135px;
		background-color: #ffffff1a;
		border-radius: 5px;
		display: flex;
		align-items: center;
		justify-content: center;
	}
    	.tileTitle {
		align-self: flex-start;
		margin-top: 10px;
		margin-left: 10px;
		margin-bottom: auto;
	}

	#tiles {
		margin: 10px;
		width: 275px;
		height: 275px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	#uvBar {
		background: linear-gradient(0deg, rgba(255, 255, 255, 0.25), rgba(255, 255, 255, 0.25)),
			linear-gradient(90deg, #00ff29 0%, #ffe70e 34%, #ff0000 70.5%, #9e00ff 100%);
		height: 5px;
		width: 115px;
		border-radius: 10px;
	}

	#uvBar {
		margin-bottom: 16%;
	}
	#uvBarBall {
		background-color: #82f21b;
		position: relative;
		bottom: 73%;
		left: 16px;
		width: 10px;
		height: 10px;
		border: 1px solid #ffffff;
		border-radius: 7px;
	}
</style>
