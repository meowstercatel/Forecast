<script>
	// @ts-nocheck

	import Counter from "./Navigation.svelte";
	import Tiles from "./Tiles.svelte";
	import Tile from "./Tile.svelte";
	import Navigation from "./Navigation.svelte";
	import WeatherBar from "./nudl/WeatherBar.svelte";
	import { onMount } from "svelte";

	let todaysWeather = [{ temp: "0", hour: "00:00" }];
	let weekWeather = [{ temp: "0", day: "09-10" }];
	let precipitationProbability = 0;
	let uvIndex = 0;
	let windSpeed = 0;
	let windDirection = "NW";
	let location = {
		container: "",
		id: "",
		latitude: 0.0,
		longitude: 0.0,
		name: "",
	};

	const id = "756135";
	class Weather {
		constructor() {
			this.response = {};
			fetchApi();
		}
		async fetchApi() {
			const request = await fetch(
				`https://weather-broker-cdn.api.bbci.co.uk/en/forecast/aggregated/${id}`,
			);
			const response = await request.json();
			this.response = response;
		}
		getWeekWeather() {
			let weekWeather = [];
			for (let i = 0; i <= 7; i++) {
				const weather = this.response.forecasts[i];
				if (weather.detailed.reports < 8) {
					weekWeather.push({
						temp: weather.detailed.reports[
							weather.detailed.reports.length - 1
						].feelsLikeTemperatureC,
						day: weather.summary.report.localDate.slice(5),
					});
				} else {
					weekWeather.push({
						temp: weather.detailed.reports[
							Math.floor(weather.detailed.reports.length / 2)
						].feelsLikeTemperatureC,
						day: weather.summary.report.localDate.slice(5),
					});
				}
			}
			return weekWeather;
		}
		getTodaysWeather() {
			let todaysWeather = [];
			this.response.forecasts[0].detailed.reports.forEach((weather) => {
			todaysWeather.push({
				temp: weather.feelsLikeTemperatureC,
				hour: weather.timeslot,
			});
			return todaysWeather;
		});
		}
	}

	onMount(async () => {
		const weather = new Weather();
		weekWeather = weather.getWeekWeather();
		todaysWeather = weather.getTodaysWeather();
		
		todaysWeather = todaysWeather;
		weekWeather = weekWeather;

	});
</script>

<svelte:head>
	<title>Weather</title>
	<meta name="description" content="weather app" />
</svelte:head>

<main>
	<Navigation />
	<div id="forecast">
		<div id="today">
			{#each todaysWeather as weather}
				<WeatherBar
					date={weather.hour}
					temperature={weather.temp + "C"}
				/>
			{/each}
		</div>
		<div id="bottom">
			<div id="multiDayForecast">
				<div
					style="gap: 10px; display: flex; flex-grow: 1; flex-shrink: 1; align-items: center; text-wrap: nowrap; width: 100%;"
				>
					7-day forecast <hr style="width: 80%;" />
				</div>
				<div class="bars">
					{#each weekWeather as weather}
						<WeatherBar
							date={weather.day}
							temperature={weather.temp + "C"}
							multiplier={6}
						/>
					{/each}
				</div>
			</div>
			<Tiles>
				<div slot="uvIndex">
					<Tile title="UV Index">
						<div><strong>1</strong> Low</div>
						<div id="uvBar">
							<div id="uvBarBall"></div>
						</div>
					</Tile>
				</div>
				<div slot="wind">
					<Tile title="Wind"></Tile>
				</div>
				<div slot="sunset">
					<Tile title="Sunset"></Tile>
				</div>
				<div slot="precipitation">
					<Tile title="Precipitation"></Tile>
				</div>
			</Tiles>
		</div>
	</div>
</main>

<style>
	#uvBar {
		background: linear-gradient(
				0deg,
				rgba(255, 255, 255, 0.25),
				rgba(255, 255, 255, 0.25)
			),
			linear-gradient(
				90deg,
				#00ff29 0%,
				#ffe70e 34%,
				#ff0000 70.5%,
				#9e00ff 100%
			);
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

	#multiDayForecast {
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 15px;
		width: 100%;
		height: 100%;
	}
	.bars {
		display: flex;
		align-items: center;
		gap: 5px;
		height: 235px;
		width: 100%;
	}
	#today {
		width: 978px;
		height: 330px;
		display: flex;
		gap: 5px;
	}
	#forecast {
		width: 998px;
		height: 642px;
		padding: 10px;
	}
	main {
		color: white;
		width: 998px;
		height: 698px;
		border-radius: 19px;
		background-color: #242424db;
		display: flex;
		flex-direction: column;
		overflow: hidden;
	}
	#bottom {
		width: 99%;
		margin-top: 10px;
		display: flex;
		align-items: center;
		justify-content: space-between;
		flex-grow: 0;
	}
</style>
