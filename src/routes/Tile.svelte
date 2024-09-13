<script>
    export let title = "UV Index";
</script>

<div class="tile" id="uvIndex">
    <div class="innerTile">
        <div class="tileTitle">{title}</div>

        <div
            style="display: flex; align-items: flex-start; gap: 10px; justify-content: center; flex-direction: column;"
        >
            <slot></slot>
            <!-- <div><strong>1</strong> Low</div>
            <div id="uvBar">
                <div id="uvBarBall"></div>
            </div> -->
        </div>
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
</style>