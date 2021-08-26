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

<!-- <div class="card bordered">
    <div class="card-body">
      <h2 class="card-title">Image bottom</h2> 
      <p>Rerum reiciendis beatae tenetur excepturi aut pariatur est eos. Sit sit necessitatibus veritatis sed molestiae voluptates incidunt iure sapiente.</p> 
      <div class="card-actions">
        <button class="btn btn-primary">Login</button> 
        <button class="btn btn-ghost">Register</button>
      </div>
    </div> 
    <figure>
      <img src="https://picsum.photos/id/1005/400/250">
    </figure>
  </div>  -->
<div class="mockup-window bg-base-300">
	<div class="card-body bg-gray-50">
		<p class="text-gray-500 font-semibold text-center">We offer 3 kinds of services.</p>
		<h4 class="card-title uppercase font-bold text-gray-600 text-center">Good × Cheap × Fast</h4>
		<p class="text-gray-500 font-semibold text-center mb-3">But you can pick only two.</p>
		<div class="tog-contaiiner mt-5">
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
		<div>
			<p class="text-center text-xs mt-8 hover:font-semibold">
				<a href="https://github.com/poonlap/gcf"> Github</a>
			</p>
			<p class="text-center text-xs hover:font-semibold">
				<a href="https://kit.svelte.dev/" class="hover:font-semibold">Svelte(kit)</a> ❤
				<a href="https://tailwindcss.com/">Tailwindcss</a>
				• <a href="https://daisyui.com/">Daisy UI</a>
			</p>
		</div>
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
