<script>
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import { onMount } from "svelte";
  import Button from "./Button.svelte";
  import AnimatedFrame from "./AnimatedFrame.svelte";

  gsap.registerPlugin(ScrollTrigger);

  let currentIndex = $state(1);
  let hasClicked = $state(false);

  let loading = $state(true);
  let loadedVideos = $state(0);

  const totalVideos = 4;
  let videoFrame;
  let previewVdRef;
  let nextVdRef;

  const handleVideoLoad = () => {
    loadedVideos += 1;
  };

  $effect(() => {
    if (loadedVideos === totalVideos - 1) {
      loading = false;
    }
  })

  const handleMiniVdClick = () => {
    hasClicked = true;
    currentIndex = (currentIndex % totalVideos) + 1;
  };

$effect(() => {
    if (hasClicked) {
      gsap.set('#next-video', {
        scale:0,
        visibility: 'visible'
      });

      gsap.to('#next-video', {
        transformOrigin: 'center center',
        scale: 1,
        width: '100%',
        height: '100%',
        duration: 1,
        ease: 'power1.inOut',
        onStart: () => nextVdRef?.play()
      });

      gsap.from('#current-video', {
        transformOrigin: 'center center',
        scale: 0,
        duration: 1.5,
        ease: 'power1.inOut'
      });
    }

    // Reading currentIndex makes this effect react to changes to it
    currentIndex;
  });
  
$effect(() => {
    if (!videoFrame) return;

    gsap.set(videoFrame, {
      clipPath: 'polygon(14% 0, 72% 0, 88% 90%, 0 95%)',
      borderRadius: '0% 0% 40% 10%'
    });

    const animation = gsap.from(videoFrame, {
      clipPath: 'polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%)',
      borderRadius: '0% 0% 0% 0%',
      ease: 'power1.inOut',
      scrollTrigger: {
        trigger: videoFrame,
        start: 'center center',
        end: 'bottom center',
        scrub: true
      }
    });

    return () => {
      animation.scrollTrigger?.kill();
      animation.kill();
    };
  });

  const getVideoSrc = (index) => `/videos/hero-${index}.mp4`;
</script>

<div class="relative h-dvh w-screen overflow-x-hidden">
  {#if loading}
    <div
      class="flex-center absolute z-100 h-dvh w-screen overflow-hidden bg-violet-50"
    >
      <div class="three-body">
        <div class="three-body__dot"></div>
        <div class="three-body__dot"></div>
        <div class="three-body__dot"></div>
      </div>
    </div>
  {/if}

  <div
    id="video-frame"
    bind:this={videoFrame}
    class="relative z-10 h-dvh w-screen overflow-hidden rounded-lg bg-blue-75"
  >
    <div>
      <div class="mask-clip-path absolute-center absolute z-50 size-64 cursor-pointer overflow-hidden rounded-lg">
      <AnimatedFrame>
      <!-- svelte-ignore a11y_no_static_element_interactions -->
        <div
          onclick={handleMiniVdClick}
          class="origin-center scale-50 opacity-0 transition-all duration-500 ease-in hover:scale-100 hover:opacity-100"
        >
          <video
            bind:this={previewVdRef}
            src={getVideoSrc((currentIndex % totalVideos) + 1)}
            loop
            muted
            id="current-video"
            class="size-64 origin-center scale-150 object-cover object-center"
            onloadeddata={handleVideoLoad}
          >Your browser does not support HTML5 video.</video>
        </div>
      </AnimatedFrame>
      </div>
      <video
      bind:this={nextVdRef}
      src={getVideoSrc(currentIndex)}
      loop
      muted
      id="next-video"
      class="absolute-center invisible absolute z-20 size-64 object-cover object-center"
      onloadeddata={handleVideoLoad}
    >
    Your browser does not support HTML5 video.
    </video>
      <video
            src={getVideoSrc(
              currentIndex === totalVideos - 1 ? 1 : currentIndex
            )}
            autoPlay
            loop
            muted
            class="absolute left-0 top-0 size-full object-cover object-center"
            onloadeddata={handleVideoLoad}
          >Your browser does not support HTML5 video.</video>
    </div>
<h1 class="special-font hero-heading absolute bottom-5 right-5 z-40 text-blue-75">
          G<b>A</b>MING
        </h1>

        <div class="absolute left-0 top-0 z-40 size-full">
          <div class="mt-24 px-5 sm:px-10">
            <h1 class="special-font hero-heading text-blue-100">
              redefi<b>n</b>e
            </h1>

            <p class="mb-5 max-w-64 font-robert-regular text-blue-100">
              Enter the Metagame Layer <br /> Unleash the Play Economy
            </p>

            <Button
              id="watch-trailer"
              title="Watch trailer"
              leftIcon=""
              containerClass="bg-yellow-300 flex-center gap-1"
            />
          </div>
        </div>
    
  </div>
  <h1 class="special-font hero-heading absolute bottom-5 right-5 text-black">
      G<b>A</b>MING
    </h1>
</div>