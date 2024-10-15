<script>
	import { onMount } from "svelte";

	export let date = 'Now';
	export let state = 'Cloudy';
	export let temperature = '25';
	export let multiplier = 9;

	let weatherBar;
	// onMount(() => setTimeout(() => {
	// 	weatherBar.style.height = parseInt(temperature)*multiplier+"px"
	// }, 2000));
	
</script>

<div class="weatherBar">
	<div class="weatherBarText">
		<div id="date">{date}</div>
		<div id="state">{state}</div>
	</div>
	<div bind:this={weatherBar} style="height: {parseInt(temperature)*multiplier}px" class="weatherYellow">
		<div style="height: 3px; width: 100%; background-color: yellow; align-self: flex-start;"></div>
		<div class="weatherBarTemperature" style="">
			{temperature}
		</div>
	</div>
</div>

<style>
	.weatherBarTemperature {
		align-self: last baseline;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		margin-top: auto;
        margin-bottom: 10px;
	}
	.weatherBar {
		font-size: 13px;
		flex-grow: 1;
		border-radius: 5px;
		height: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		flex-direction: column;
		border-radius: 5px;
		background: #ffffff1a;
	}
	.weatherYellow {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #ffb80040;
		width: 100%;
		border-radius: 5px;
		height: 54%;
	}
	.weatherBarText {
		margin-top: 10px;
		display: flex;
		flex-direction: column;
		gap: 10px;
		align-items: center;
		justify-content: center;
	}
</style>
