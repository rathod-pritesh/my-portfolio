<script>
	import Background3D from "../components/Background3D.svelte";
	import "../app.css";
	import { goto } from "$app/navigation";
	import { page } from "$app/state";

	let { children } = $props();

	const navItems = [
		{ name: "Home", path: "/" },
		{ name: "About", path: "/about" },
		{ name: "Projects", path: "/projects" },
		{ name: "Contact", path: "/contact" }
	];

	const currentPath = $derived(page.url.pathname);
</script>

<div class="relative w-screen h-screen overflow-hidden">

	<div class="absolute inset-0 z-0 pointer-events-none">
    <Background3D />
  </div>

	<!-- Navbar -->
	<nav class="fixed top-6 left-1/2 -translate-x-1/2 z-50">
		<div class="flex gap-8 px-8 py-3 rounded-full backdrop-blur-md bg-white/10 border border-white/20 shadow-lg">
			{#each navItems as item}
				<button 
					onclick={() => goto(item.path)}
					class="
					relative cursor-pointer font-medium tracking-wide transition-all duration-300 
					{currentPath === item.path 
						? 'text-cyan-400'
						: 'text-white hover:text-cyan-400'}
					"
				>
				{item.name}

				<!-- Active underline -->
				<span
				class="
					absolute left-0 -bottom-1 h-0.5 bg-cyan-400 transition-all duration-300
              {currentPath === item.path ? 'w-full' : 'w-0 group-hover:w-full'}
				"
				></span>
				</button>
			{/each}
		</div>
	</nav>

	<!-- Page Content -->
	<div class="relative z-10">
		{@render children()}
	</div>
</div>
