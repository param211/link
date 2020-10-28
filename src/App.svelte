<script>
	let url
	let customString
	let result = null
	
	async function doPost () {
		const res = await fetch('https://murmuring-retreat-87582.herokuapp.com/', {
			method: 'POST',
			mode: 'cors', // no-cors, *cors, same-origin
    		cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
    		credentials: 'same-origin', // include, *same-origin, omit
    		headers: {
      			'Content-Type': 'application/json'
      			// 'Content-Type': 'application/x-www-form-urlencoded',
    		},
    		redirect: 'follow', // manual, *follow, error
    		referrerPolicy: 'no-referrer',
			body: JSON.stringify({
				url: url,
				custom_target: customString
			}),
		})
		
		const json = await res.json()
		// result = JSON.stringify(json)
		result = json
	}
</script>


<main>
	<h2>URL Shortener</h2>
	<input bind:value={url} placeholder="Enter URL here" />
	<input bind:value={customString} placeholder="Custom string (optional)"/>
	<button type="button" on:click={doPost}>
		Shorten
	</button>
	{#if result != null}
		<p>
			Shortened URL:
		</p>
		<pre>
		{"https://link.paramchauhan.com/" + result['short']}
		</pre>
	{/if}
</main>


<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h2 {
		color: #ff3e00;
		font-size: 3em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>