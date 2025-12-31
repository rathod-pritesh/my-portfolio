<script>
	import Background3D from "../components/Background3D.svelte";
	import "../app.css";

	let { children } = $props();
</script>

<div class="relative w-screen h-screen overflow-hidden">
	<div class="absolute inset-0 z-0 pointer-events-none">
    <Background3D />
  </div>

	<!-- Page Content -->
	<div class="relative z-10">
		{@render children()}
	</div>
</div>
