<script>
  let itemRef;
  let transformStyle = "";

  function handleMouseMove(event) {
    if (!itemRef) return;

    const { left, top, width, height } = itemRef.getBoundingClientRect();

    const relativeX = (event.clientX - left) / width;
    const relativeY = (event.clientY - top) / height;

    const tiltX = (relativeY - 0.5) * 5;
    const tiltY = (relativeX - 0.5) * -5;

    transformStyle = `
      perspective(700px)
      rotateX(${tiltX}deg)
      rotateY(${tiltY}deg)
      scale3d(.95, .95, .95)
    `;
  }

  function handleMouseLeave() {
    transformStyle = "";
  }
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<!-- svelte-ignore a11y_click_events_have_key_events -->

<div
  bind:this={itemRef}
  class={$$props.class}
  style:transform={transformStyle}
  onmousemove={handleMouseMove}
  onmouseleave={handleMouseLeave}
>
  <slot />
</div>
