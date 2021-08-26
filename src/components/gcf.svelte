<script>
	let gcf = { g: false, c: false, f: false };
	let atLeastTwo = false;
	let lastClick = 'none';
	function onClick(event) {
		let before = gcf[event.target.id];
		// console.log('Source ' + event.target.id + ' ' + gcf[event.target.id]);
		gcf[event.target.id] = !gcf[event.target.id];
		let after = gcf[event.target.id];
		// console.log('After clicked: Source ' + event.target.id + ' ' + gcf[event.target.id]);
		// Update DOM
		if (atLeastTwo && !before) {
			// console.log('[ACTION] Turn some toggle OFF.');
			gcf[randomTurnOn(event.target.id)] = false;
		}
		atLeastTwo = gcf.g ? gcf.c || gcf.f : gcf.c && gcf.f;
		setTimeout(() => {
			event.target.checked = gcf[event.target.id];
		}, 0);
		lastClick = event.target.id;
	}

	function randomTurnOn(caller) {
		let name = ['g', 'c', 'f'];
		let num = 0;
		while (true) {
			num = Math.floor(Math.random() * 3);
			if (name[num] != caller) {
				return name[num];
			}
		}
	}
</script>

<div>
	<div class="tog-contaiiner">
		<input
			id="g"
			type="checkbox"
			class="toggle toggle-lg toggle-primary drop-shadow-lg"
			bind:checked={gcf.g}
			on:click|preventDefault={onClick}
		/> <span class="text text-primary">Good</span>
	</div>
	<div class="tog-contaiiner">
		<input
			id="c"
			type="checkbox"
			class="toggle toggle-lg toggle-secondary drop-shadow-lg"
			bind:checked={gcf.c}
			on:click|preventDefault={onClick}
		/>
		<span class="text text-secondary">Cheap</span>
	</div>
	<div class="tog-contaiiner">
		<input
			id="f"
			type="checkbox"
			class="toggle toggle-lg toggle-accent drop-shadow-lg"
			bind:checked={gcf.f}
			on:click|preventDefault={onClick}
		/> <span class="text text-accent">Fast</span>
	</div>
</div>

<!-- <div>
<p>At least two: {atLeastTwo}</p>
<p>Last clicked: {lastClick}</p>
</div> -->
<style>
    .tog-contaiiner {
        @apply flex items-center mb-2;
    }
	.tog {
		@apply toggle toggle-lg;
	}
	.text {
		@apply uppercase font-bold text-xl ml-3;
	}
</style>
