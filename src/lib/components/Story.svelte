<script>
  import gsap from "gsap";

  import Button from "./Button.svelte";
  import AnimatedTitle from "./AnimatedTitle.svelte";

  let frameRef;

  function handleMouseMove(e) {
    const { clientX, clientY } = e;
    const element = frameRef;

    if (!element) return;

    const rect = element.getBoundingClientRect();

    const xPos = clientX - rect.left;
    const yPos = clientY - rect.top;

    const centerX = rect.width / 2;
    const centerY = rect.height / 2;

    const rotateX = ((yPos - centerY) / centerY) * -10;
    const rotateY = ((xPos - centerX) / centerX) * 10;

    gsap.to(element, {
      duration: 0.3,
      rotateX,
      rotateY,
      transformPerspective: 500,
      ease: "power1.inOut",
    });
  }

  function handleMouseLeave() {
    const element = frameRef;

    if (!element) return;

    gsap.to(element, {
      duration: 0.3,
      rotateX: 0,
      rotateY: 0,
      ease: "power1.inOut",
    });
  }
</script>

<div id="story" class="min-h-dvh w-screen bg-black text-blue-50">
  <div class="flex size-full flex-col items-center py-10 pb-24">
    <p class="font-general text-sm uppercase md:text-[10px]">
      the multiversal ip world
    </p>

    <div class="relative size-full">
      <AnimatedTitle
        title="the st<b>o</b>ry of <br /> a hidden real<b>m</b>"
        containerClass="mt-5 pointer-events-none mix-blend-difference relative z-10"
      />

      <div class="story-img-container">
        <div class="story-img-mask">
          <div class="story-img-content">
            <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
            <img
              bind:this={frameRef}
              onmousemove={handleMouseMove}
              onmouseleave={handleMouseLeave}
              onmouseup={handleMouseLeave}
              onmouseenter={handleMouseLeave}
              src="/img/entrance.webp"
              alt="entrance.webp"
              class="object-contain"
            />
          </div>
        </div>

        <!-- for the rounded corner -->
        <svg
          class="invisible absolute size-0"
          xmlns="http://www.w3.org/2000/svg"
        >
          <defs>
            <filter id="flt_tag">
              <feGaussianBlur
                in="SourceGraphic"
                stdDeviation="8"
                result="blur"
              />

              <feColorMatrix
                in="blur"
                mode="matrix"
                values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 19 -9"
                result="flt_tag"
              />

              <feComposite in="SourceGraphic" in2="flt_tag" operator="atop" />
            </filter>
          </defs>
        </svg>
      </div>
    </div>

    <div
      class="-mt-80 flex w-full justify-center md:-mt-64 md:me-44 md:justify-end"
    >
      <div class="flex h-full w-fit flex-col items-center md:items-start">
        <p
          class="mt-3 max-w-sm text-center font-circular-web text-violet-50 md:text-start"
        >
          Where realms converge, lies Zentry and the boundless pillar. Discover
          its secrets and shape your fate amidst infinite opportunities.
        </p>

        <Button
          id="realm-btn"
          title="discover prologue"
          containerClass="mt-5"
        />
      </div>
    </div>
  </div>
</div>
