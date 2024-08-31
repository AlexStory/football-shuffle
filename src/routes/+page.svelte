<script lang="ts">
	type Game = {
		teams: string[];
		year: number;
		week: number;
	};
	import data2023 from '../lib/data/2023';

	const data = data2023;

	let teams: string[] = $state([
		'Arizona Cardinals',
		'Atlanta Falcons',
		'Baltimore Ravens',
		'Buffalo Bills',
		'Carolina Panthers',
		'Chicago Bears',
		'Cincinnati Bengals',
		'Cleveland Browns',
		'Dallas Cowboys',
		'Denver Broncos',
		'Detroit Lions',
		'Green Bay Packers',
		'Houston Texans',
		'Indianapolis Colts',
		'Jacksonville Jaguars',
		'Kansas City Chiefs',
		'Las Vegas Raiders',
		'Los Angeles Chargers',
		'Los Angeles Rams',
		'Miami Dolphins',
		'Minnesota Vikings',
		'New England Patriots',
		'New Orleans Saints',
		'New York Giants',
		'New York Jets',
		'Philadelphia Eagles',
		'Pittsburgh Steelers',
		'San Francisco 49ers',
		'Seattle Seahawks',
		'Tampa Bay Buccaneers',
		'Tennessee Titans',
		'Washington Commanders'
	]);
	let selectedTeam = $state('');
	let selectedYear = $state('');

	let filtered = $derived(
		data.filter((game) => {
			if (selectedTeam && selectedYear) {
				return game.teams.includes(selectedTeam) && game.year * 1 === +selectedYear;
			} else if (selectedTeam) {
				return game.teams.includes(selectedTeam);
			} else {
				return game;
			}
		})
	);

	let selectedGame: Game = $state({ teams: [], year: 0, week: 0 });

	function shuffle() {
		const randomIndex = Math.floor(Math.random() * filtered.length);
		const randomGame = filtered[randomIndex];
		selectedGame = randomGame;
	}
</script>

<svelte:head>
	<title>Football Shuffle</title>
	<meta name="description" content="Football Shuffle" />
</svelte:head>

<section>
	<p>Optionally pick a team, and year and get a random game picked to watch!</p>

	<div>
		<label for="team">Team:</label>
		<select bind:value={selectedTeam} name="team">
			{#each teams as team}
				<option value={team}>{team}</option>
			{/each}
		</select>
		<button onclick={() => (selectedTeam = '')}>Clear</button>
	</div>

	<div>
		<label for="year">Year:</label>
		<select bind:value={selectedYear} name="year">
			{#each Array.from({ length: 2024 - 2008 }, (_, i) => new Date().getFullYear() - i) as year}
				<option value={year}>{year}</option>
			{/each}
		</select>
		<button onclick={() => (selectedYear = '')}>Clear</button>
	</div>

	<button onclick={shuffle} class="shuffle"> SHUFFLE! </button>

	{#if selectedGame.year > 0}
		<p>{selectedGame.teams[0]}</p>
		<p>vs</p>
		<p>{selectedGame.teams[1]}</p>
		<p>{selectedGame.year}</p>
		<p>week: {selectedGame.week}</p>
	{/if}
</section>

<style>
	button {
		cursor: pointer;
		background-color: #3498db;
		font-weight: bold;
		color: white;
		border: none;
		border-radius: 8px;
		padding: 5px 8px;
	}

	p {
		border-bottom: 1px solid #ccc;
	}

	select {
		background-color: white;
		border: 1px solid #ccc;
		padding: 5px;
		border-radius: 2px;
	}

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	.shuffle {
		min-width: 200px;
		margin-top: 10px;
		padding-top: 15px;
		padding-bottom: 15px;
	}
</style>
