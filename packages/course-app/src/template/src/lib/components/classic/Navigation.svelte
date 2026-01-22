<script lang="ts">
  import { onMount } from 'svelte';
  import { Close } from 'carbon-icons-svelte';
  import Menu from 'carbon-icons-svelte/lib/Menu.svelte';

  const brandFullText = "School of Tomorrow's AI";
  let brandText = $state('');

  let open = $state(false); // State for mobile menu

  // Function to toggle the mobile menu
  function toggleMenu() {
    open = !open;
  }

  // Typewriter animation for brand text
  onMount(() => {
    let index = 0;
    const interval = setInterval(() => {
      if (index < brandFullText.length) {
        brandText += brandFullText[index];
        index += 1;
      } else {
        clearInterval(interval);
      }
    }, 80);

    return () => clearInterval(interval);
  });
</script>

<header class="classic-header border-b border-gray-100 bg-white">
  <div class="mx-auto flex max-w-6xl items-center justify-between px-4 py-4 lg:px-8">
    <!-- Left: Logo + Brand -->
    <a href="/" class="flex items-center gap-2">
      <img src="/logo.svg" alt="School of Tomorrow's AI logo" class="h-7 w-auto" />
      <span class="relative inline-block">
        <!-- Invisible text that reserves the full width of the brand -->
        <span
          class="pointer-events-none select-none text-base font-medium tracking-tight text-[#22113E] opacity-0"
          aria-hidden="true"
        >
          {brandFullText}
        </span>

        <!-- Absolutely positioned animated text on top -->
        <span
          class="absolute inset-0 text-base font-medium tracking-tight text-[#22113E]"
          aria-label="School of Tomorrow's AI"
        >
          {brandText}
        </span>
      </span>
    </a>

    <!-- Desktop Navigation (Hidden on mobile) -->
    <nav class="hidden items-center gap-6 md:flex">
      <a href="/courses" class="classic-nav-link"> Courses </a>
      <a href="/blog" class="classic-nav-link"> Blog </a>
    </nav>

    <!-- Desktop CTA Button (Hidden on mobile) -->
    <a href="/courses" class="start-learning-btn classic-primary-btn hidden md:inline-flex">
      Start Learning
    </a>

    <!-- Mobile Menu Button (Visible only on mobile) -->
    <button onclick={toggleMenu} class="md:hidden" aria-label="Toggle menu" type="button">
      <Menu size={24} class="text-[#22113E]" />
    </button>
  </div>

  <!-- Mobile Sidebar Menu (Visible only on mobile) -->
  {#if open}
    <div
      class="fixed inset-0 z-50 bg-white md:hidden"
      role="dialog"
      aria-modal="true"
      aria-label="Navigation menu"
      tabindex="-1"
      onclick={(e) => {
        if (e.target === e.currentTarget) toggleMenu();
      }}
      onkeydown={(e) => {
        if (e.key === 'Escape') toggleMenu();
      }}
    >
      <div class="flex h-full flex-col pt-16">
        <button
          onclick={toggleMenu}
          class="absolute right-4 top-4 z-20"
          aria-label="Close menu"
          type="button"
        >
          <Close size={24} class="text-[#22113E]" />
        </button>

        <nav class="flex flex-col px-6">
          <a
            href="/courses"
            onclick={toggleMenu}
            class="classic-nav-link-mobile border-b border-gray-100 px-0 py-4"
          >
            Courses
          </a>
          <a
            href="/blog"
            onclick={toggleMenu}
            class="classic-nav-link-mobile border-b border-gray-100 px-0 py-4"
          >
            Blog
          </a>
          <a
            href="/courses"
            onclick={toggleMenu}
            class="start-learning-btn classic-primary-btn mt-4 inline-flex items-center justify-center"
          >
            Start Learning
          </a>
        </nav>
      </div>
    </div>
  {/if}
</header>

<style>
  /* School of Tomorrow's AI Header Styles */
  .classic-header {
    position: relative;
    font-family:
      'Space Grotesk',
      system-ui,
      -apple-system,
      BlinkMacSystemFont,
      'Segoe UI',
      sans-serif;
  }

  .classic-header a,
  .classic-header nav,
  .classic-header button {
    font-family:
      'Space Grotesk',
      system-ui,
      -apple-system,
      BlinkMacSystemFont,
      'Segoe UI',
      sans-serif;
  }

  /* Desktop Navigation Links */
  .classic-header .classic-nav-link {
    color: #22113e;
    text-decoration: none;
    font-size: 0.875rem;
    font-weight: 500;
    transition:
      color 150ms ease,
      border-color 150ms ease;
    border-bottom: 2px solid transparent;
    padding-bottom: 2px;
  }

  .classic-header .classic-nav-link:hover,
  .classic-header .classic-nav-link:focus-visible {
    color: #ea7dff;
    border-bottom-color: #ea7dff;
  }

  /* Mobile Navigation Links */
  .classic-header .classic-nav-link-mobile {
    color: #22113e;
    text-decoration: none;
    font-size: 1rem;
    font-weight: 500;
    transition: color 150ms ease;
  }

  .classic-header .classic-nav-link-mobile:hover,
  .classic-header .classic-nav-link-mobile:focus-visible {
    color: #ea7dff;
  }

  /* Start Learning Button - layout/alignment only */
  /* Visual styles (color, padding, hover) come from .classic-primary-btn in app.css */
</style>
