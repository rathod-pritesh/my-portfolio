<script>
  import profile from "$lib/assets/portrait.png";
</script>

<section
  id="home"
  class="relative min-h-screen flex items-center justify-center overflow-hidden px-6"
>

  <!-- Content Wrapper -->
  <div class="relative z-40 w-full max-w-7xl flex flex-col-reverse md:flex-row items-center justify-between gap-12">

    <!-- LEFT TEXT -->
    <div class="text-center md:text-left max-w-xl">
      <h1 class="text-4xl sm:text-5xl md:text-6xl font-bold text-white">
        Hi, I'm Pritesh 👋
      </h1>

      <p class="mt-4 text-gray-300 text-base sm:text-lg">
        Building immersive web experiences
      </p>
    </div>

    <div class="relative flex justify-center items-center">

      <div
        class="absolute w-[260px] h-[260px] sm:w-[320px] sm:h-[320px] rounded-full bg-cyan-400/10 blur-3xl z-10"
      ></div>

      <img
        src={profile}
        alt="Pritesh"
        class="relative z-20
               w-[240px] h-[240px]
               sm:w-[300px] sm:h-[300px]
               md:w-[360px] md:h-[360px]
               rounded-full
               object-cover
               border-4 border-white/10
               shadow-2xl
               pointer-events-none select-none"
      />
    </div>

  </div>
</section>
