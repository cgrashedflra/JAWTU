<script>
  const socialLinks = [
    {
      href: "https://discord.com",
      label: "Discord",
      icon: "discord",
    },
    {
      href: "https://twitter.com",
      label: "Twitter",
      icon: "twitter",
    },
    {
      href: "https://youtube.com",
      label: "YouTube",
      icon: "youtube",
    },
    {
      href: "https://medium.com",
      label: "Medium",
      icon: "medium",
    },
  ];
</script>

<footer class="w-screen bg-[#5542ff] py-4 text-black">
  <div
    class="container mx-auto flex flex-col items-center justify-between gap-4 px-4 md:flex-row"
  >
    <p class="text-center text-sm font-light md:text-left">
      ©Nova 2024. All rights reserved
    </p>

    <div class="flex justify-center gap-4 md:justify-start">
      {#each socialLinks as link}
        <a
          href={link.href}
          target="_blank"
          rel="noopener noreferrer"
          aria-label={link.label}
          class="text-black transition-colors duration-500 ease-in-out hover:text-white"
        >
          {#if link.icon === "discord"}
            <svg
              viewBox="0 0 24 24"
              class="h-5 w-5"
              fill="currentColor"
              aria-hidden="true"
            >
              <path
                d="M19.54 5.05A16.9 16.9 0 0 0 15.32 3.74l-.52 1.06a15.8 15.8 0 0 0-5.6 0l-.52-1.06A16.9 16.9 0 0 0 4.46 5.05C1.79 9.02 1.07 12.89 1.43 16.7a17 17 0 0 0 5.2 2.63l1.26-1.72a10.5 10.5 0 0 1-1.98-.96l.49-.37c3.83 1.79 7.98 1.79 11.76 0l.49.37c-.63.37-1.29.69-1.98.96l1.26 1.72a17 17 0 0 0 5.2-2.63c.43-4.41-.73-8.24-2.59-11.65ZM8.62 14.48c-1.18 0-2.15-1.09-2.15-2.43s.95-2.43 2.15-2.43c1.21 0 2.17 1.09 2.15 2.43 0 1.34-.95 2.43-2.15 2.43Zm6.76 0c-1.18 0-2.15-1.09-2.15-2.43s.95-2.43 2.15-2.43c1.21 0 2.17 1.09 2.15 2.43 0 1.34-.95 2.43-2.15 2.43Z"
              />
            </svg>
          {:else if link.icon === "twitter"}
            <svg
              viewBox="0 0 24 24"
              class="h-5 w-5"
              fill="currentColor"
              aria-hidden="true"
            >
              <path
                d="M18.9 2H22l-6.77 7.74L23.2 22h-6.24l-4.89-6.4L6.47 22H3.36l7.24-8.28L2.8 2h6.4l4.42 5.84L18.9 2Zm-1.1 17.75h1.73L8.27 4.13H6.41L17.8 19.75Z"
              />
            </svg>
          {:else if link.icon === "youtube"}
            <svg
              viewBox="0 0 24 24"
              class="h-5 w-5"
              fill="currentColor"
              aria-hidden="true"
            >
              <path
                d="M23.5 6.19a3 3 0 0 0-2.11-2.12C19.53 3.5 12 3.5 12 3.5s-7.53 0-9.39.57A3 3 0 0 0 .5 6.19C0 8.05 0 12 0 12s0 3.95.5 5.81a3 3 0 0 0 2.11 2.12c1.86.57 9.39.57 9.39.57s7.53 0 9.39-.57a3 3 0 0 0 2.11-2.12C24 15.95 24 12 24 12s0-3.95-.5-5.81ZM9.55 15.93V8.07L16.27 12l-6.72 3.93Z"
              />
            </svg>
          {:else if link.icon === "medium"}
            <svg
              viewBox="0 0 24 24"
              class="h-5 w-5"
              fill="currentColor"
              aria-hidden="true"
            >
              <path
                d="M2.01 6.34c.02-.19-.05-.38-.2-.51L.3 4.1V3.76h4.7l3.63 7.96 3.19-7.96h4.48v.34l-1.3 1.25c-.11.08-.17.21-.15.34v9.9c-.02.13.04.26.15.34l1.27 1.25v.34H9.87v-.34l1.31-1.28c.13-.13.13-.17.13-.34V7.56L7.67 17.5h-.49L2.97 7.56v6.67c-.04.23.04.47.2.64l1.7 2.06v.34H.05v-.34l1.7-2.06c.16-.17.25-.41.21-.64V6.34h.05Z"
              />
            </svg>
          {/if}
        </a>
      {/each}
    </div>

    <a
      href="#privacy-policy"
      class="text-center text-sm font-light hover:underline md:text-right"
    >
      Privacy Policy
    </a>
  </div>
</footer>
