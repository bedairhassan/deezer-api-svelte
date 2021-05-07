<script>


	async function fetchNews() {
		let url = "https://deezerdevs-deezer.p.rapidapi.com/search?q=eminem";

		var res = await fetch(url, {
			method: "GET",
			headers: {
				"x-rapidapi-key":
					"88596f40b3mshde19e870a72b70ap1a25edjsnf9709dcd3c67",
				"x-rapidapi-host": "deezerdevs-deezer.p.rapidapi.com",
			},
		});
		res = await res.json();
		let songs = await res.data;
		
		// more variables

		return songs;
	}

	let promise = fetchNews();

	function handleClick() {
		promise = fetchNews();
	}
</script>

<main>
	<h1>Welcome. Deezer API</h1>
	{#await promise}
		<p>...waiting</p>
	{:then articles}


		<table>
			<tr></tr>
		</table>

		<table class="table">
			{#each articles as article}
				<tr>
					<td>
						<img src={article.album.cover}  />
					</td>
					<td>{article.album.title}</td>
					<td>{article.title}</td>
					<!-- <td>{article.artist.name}</td> -->
				</tr>
			{/each}
		</table>
	{:catch error}
		<p style="color: red">{error.message}</p>
	{/await}
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
