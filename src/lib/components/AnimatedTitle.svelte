<script>
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";

  gsap.registerPlugin(ScrollTrigger);

  let { title, containerClass = "" } = $props();

  let containerRef;

  $effect(() => {
    if (!containerRef) return;

    const ctx = gsap.context(() => {
      const titleAnimation = gsap.timeline({
        scrollTrigger: {
          trigger: containerRef,
          start: "100 bottom",
          end: "center bottom",
          toggleActions: "play none none reverse",
        },
      });

      titleAnimation.to(
        ".animated-word",
        {
          opacity: 1,
          transform: "translate3d(0, 0, 0) rotateY(0deg) rotateX(0deg)",
          ease: "power2.inOut",
          stagger: 0.02,
        },
        0,
      );
    }, containerRef);

    return () => ctx.revert();
  });
</script>

<div bind:this={containerRef} class="animated-title {containerClass}">
  {#each title.split("<br />") as line}
    <div class="flex-center max-w-full flex-wrap gap-2 px-10 md:gap-3">
      {#each line.split(" ") as word}
        <span class="animated-word">
          {@html word}
        </span>
      {/each}
    </div>
  {/each}
</div>
