<script>
  import { onMount } from "svelte";

	onMount(() => {
		document.getElementById("close").addEventListener("click", () => {
			window.close();
		})
	})
</script>
<style>
	nav {
		-webkit-app-region: drag; margin-top: 4px; height: 56px; display: flex; align-items: center; justify-content: space-between; flex-shrink: 0; padding-left: 10px; padding-right: 10px;
	}
	.button {
		width: 24px; height: 24px; display: flex; align-items: center; justify-content: center; border-radius: 5px; padding: 10px; background-color: #FFFFFF1A;
	}
	#search {
		background-color: #00000040; width: 200px; height: 26px; padding: 10px; border-radius: 10px; box-shadow: 0px 5px 5px 0px #00000040 inset; display: flex; align-items: center; justify-content: flex-start; padding: 10px;
	}
	#windowControl {
		-webkit-app-region: no-drag;
		user-select: none;
	}
	#search {
		-webkit-app-region: no-drag;
	}
</style>

<nav>
	<div id="windowControl">
		<div class="button" id="close">X</div>
	</div>
	<div id="stats">Warsaw 26C Mostly cloudy</div>
	<div contenteditable="true" id="search">Search...</div>
</nav>