<script>
</script>

<header>
	<nav>
		<ul>
			<li>
				<a href="/">
					<h2>Football Shuffle</h2>
				</a>
			</li>
		</ul>
	</nav>
</header>

<style>
	header {
		background-color: #27ae60;
		display: flex;
		justify-content: space-between;
	}

	nav {
		display: flex;
		justify-content: center;
		margin-left: auto;
		margin-right: auto;
		--background: rgba(255, 255, 255, 0.7);
	}

	ul {
		position: relative;
		padding: 0;
		margin: 0;
		height: 3em;
		display: flex;
		justify-content: center;
		align-items: center;
		list-style: none;
		background: var(--background);
		background-size: contain;
	}

	li {
		position: relative;
		height: 100%;
	}

	nav a {
		display: flex;
		height: 100%;
		align-items: center;
		padding: 0 0.5rem;
		color: var(--color-text);
		font-weight: 700;
		font-size: 0.8rem;
		text-transform: uppercase;
		letter-spacing: 0.1em;
		text-decoration: none;
		transition: color 0.2s linear;
	}

	a:hover {
		color: var(--color-theme-1);
	}
</style>
