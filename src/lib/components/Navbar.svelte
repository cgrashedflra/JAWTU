<script>
  import Button from "./Button.svelte";
  import { onMount } from "svelte";
  import gsap from "gsap";

  const navItems = ["Nexus", "Vault", "Prologue", "About", "Contact"];

  let isAudioPlaying = $state(false);
  let isIndicatorActive = $state(false);
  let isNavVisible = $state(true);

  let audioElement;
  let navContainer;

  function toggleAudioIndicator() {
    isAudioPlaying = !isAudioPlaying;
    isIndicatorActive = !isIndicatorActive;

    if (isAudioPlaying) {
      audioElement?.play();
    } else {
      audioElement?.pause();
    }
  }

  $effect(() => {
    if (!navContainer) return;

    gsap.to(navContainer, {
      y: isNavVisible ? 0 : -100,
      duration: 0.35,
      ease: "power3.out",
      overwrite: true,
    });
  });

  onMount(() => {
    let lastScrollY = window.scrollY;

    const handleScroll = () => {
      const currentScrollY = window.scrollY;

      if (currentScrollY <= 10) {
        isNavVisible = true;
        navContainer?.classList.remove("floating-nav");
      } else if (currentScrollY > lastScrollY) {
        // scrolling down
        isNavVisible = false;
        navContainer?.classList.add("floating-nav");
      } else if (currentScrollY < lastScrollY) {
        // scrolling up
        isNavVisible = true;
        navContainer?.classList.add("floating-nav");
      }

      lastScrollY = currentScrollY;
    };

    window.addEventListener("scroll", handleScroll, { passive: true });

    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  });
</script>

<div
  bind:this={navContainer}
  class="fixed inset-x-0 top-4 z-50 h-16 border-none transition-all duration-700 sm:inset-x-6"
>
  <header class="absolute top-1/2 w-full -translate-y-1/2">
    <nav class="flex size-full items-center justify-between p-4">
      <!-- Logo and Product button -->
      <div class="flex items-center gap-7">
        <img src="/img/logo.png" alt="logo" class="w-10" />

        <Button
          id="product-button"
          title="Products"
          containerClass="bg-blue-50 md:flex hidden items-center justify-center gap-1"
        >
          <span slot="rightIcon">→</span>
        </Button>
      </div>

      <!-- Navigation Links and Audio Button -->
      <div class="flex h-full items-center">
        <div class="hidden md:block">
          {#each navItems as item}
            <a href={`#${item.toLowerCase()}`} class="nav-hover-btn">
              {item}
            </a>
          {/each}
        </div>

        <button
          type="button"
          onclick={toggleAudioIndicator}
          class="ml-10 flex items-center space-x-0.5"
          aria-label={isAudioPlaying ? "Pause audio" : "Play audio"}
        >
          <audio
            bind:this={audioElement}
            class="hidden"
            src="/audio/loop.mp3"
            loop
          ></audio>

          {#each [1, 2, 3, 4] as bar}
            <div
              class:active={isIndicatorActive}
              class="indicator-line"
              style={`animation-delay: ${bar * 0.1}s`}
            ></div>
          {/each}
        </button>
      </div>
    </nav>
  </header>
</div>
