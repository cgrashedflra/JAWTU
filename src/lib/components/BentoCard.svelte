<script>
  export let src;
  export let title = "";
  export let description = "";
  export let isComingSoon = false;

  let cursorPosition = { x: 0, y: 0 };
  let hoverOpacity = 0;
  let hoverButtonRef;

  function handleMouseMove(event) {
    if (!hoverButtonRef) return;

    const rect = hoverButtonRef.getBoundingClientRect();

    cursorPosition = {
      x: event.clientX - rect.left,
      y: event.clientY - rect.top,
    };
  }

  function handleMouseEnter() {
    hoverOpacity = 1;
  }

  function handleMouseLeave() {
    hoverOpacity = 0;
  }
</script>

<div class="relative size-full">
  <video
    {src}
    loop
    muted
    autoplay
    playsinline
    class="absolute left-0 top-0 size-full object-cover object-center"
  ></video>

  <div
    class="relative z-10 flex size-full flex-col justify-between p-5 text-blue-50"
  >
    <div>
      <h1 class="bento-title special-font">{@html title}</h1>

      {#if description}
        <p class="mt-3 max-w-64 text-xs md:text-base">
          {description}
        </p>
      {/if}
    </div>

    {#if isComingSoon}
      <!-- svelte-ignore a11y_no_static_element_interactions -->
      <!-- svelte-ignore a11y_click_events_have_key_events -->
      <div
        bind:this={hoverButtonRef}
        onmousemove={handleMouseMove}
        onmouseenter={handleMouseEnter}
        onmouseleave={handleMouseLeave}
        class="border-hsla relative flex w-fit cursor-pointer items-center gap-1 overflow-hidden rounded-full bg-black px-5 py-2 text-xs uppercase text-white/20"
      >
        <div
          class="pointer-events-none absolute -inset-px transition duration-300"
          style="
            opacity: {hoverOpacity};
            background: radial-gradient(
              100px circle at
              {cursorPosition.x}px {cursorPosition.y}px,
              #656fe288,
              #00000026
            );
          "
        ></div>

        <!-- Location arrow -->
        <svg
          class="relative z-20 h-4 w-4"
          viewBox="0 0 24 24"
          fill="currentColor"
        >
          <path
            d="M12 2L3 21l9-4 9 4-9-19zm0 5.2l3.9 8.2L12 13.7l-3.9 1.7L12 7.2z"
          />
        </svg>

        <p class="relative z-20">coming soon</p>
      </div>
    {/if}
  </div>
</div>
