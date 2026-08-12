<script>
  import { gsap } from "gsap";

  let { children } = $props();

  let sectionRef;
  let contentRef;

  const handleMouseMove = ({ clientX, clientY, currentTarget }) => {
    const rect = currentTarget.getBoundingClientRect();

    const xOffset = clientX - (rect.left + rect.width / 2);
    const yOffset = clientY - (rect.top + rect.height / 2);

    gsap.to(sectionRef, {
      x: xOffset,
      y: yOffset,
      rotationY: xOffset / 2,
      rotationX: -yOffset / 2,
      transformPerspective: 500,
      duration: 1,
      ease: "power1.out",
    });

    gsap.to(contentRef, {
      x: -xOffset,
      y: -yOffset,
      duration: 1,
      ease: "power1.out",
    });
  };

  const handleMouseLeave = () => {
    gsap.to(sectionRef, {
      x: 0,
      y: 0,
      rotationY: 0,
      rotationX: 0,
      duration: 1,
      ease: "power1.out",
    });

    gsap.to(contentRef, {
      x: 0,
      y: 0,
      duration: 1,
      ease: "power1.out",
    });
  };
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<section
  bind:this={sectionRef}
  onmousemove={handleMouseMove}
  onmouseleave={handleMouseLeave}
  class="absolute z-50 size-full overflow-hidden rounded-lg"
  style="perspective: 500px;"
>
  <div
    bind:this={contentRef}
    class="origin-center rounded-lg"
    style="transform-style: preserve-3d;"
  >
    {@render children?.()}
  </div>
</section>