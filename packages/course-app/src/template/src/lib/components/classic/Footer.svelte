<script lang="ts">
  import { getPageSection } from '@/utils/helpers/page';
  import { sharedPage } from '@/utils/stores/pages';
  import { SECTION } from '@/utils/constants/page';

  const content = $derived(getPageSection($sharedPage, SECTION.FOOTER));
</script>

{#if content?.show}
  <nav class="classic-footer flex w-full flex-col items-center gap-4 bg-white px-6 py-4 md:flex-row md:items-center">
    <!-- Left: Empty spacer for centering balance -->
    <div class="flex-1"></div>

    <!-- Center: Social Icons (perfectly centered) -->
    <div class="social-icons flex flex-none items-center justify-center gap-6">
      <a
        href="https://www.instagram.com/lilo.think/"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Follow on Instagram"
      >
        <svg
          class="social-icon"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <rect x="2" y="2" width="20" height="20" rx="5" ry="5" />
          <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z" />
          <line x1="17.5" y1="6.5" x2="17.51" y2="6.5" />
        </svg>
      </a>
      <a
        href="https://www.youtube.com/@lina_lopes"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Subscribe on YouTube"
      >
        <svg
          class="social-icon"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <path d="M22.54 6.42a2.78 2.78 0 0 0-1.94-2C18.88 4 12 4 12 4s-6.88 0-8.6.46a2.78 2.78 0 0 0-1.94 2A29 29 0 0 0 1 11.75a29 29 0 0 0 .46 5.33A2.78 2.78 0 0 0 3.4 19c1.72.46 8.6.46 8.6.46s6.88 0 8.6-.46a2.78 2.78 0 0 0 1.94-2 29 29 0 0 0 .46-5.25 29 29 0 0 0-.46-5.33z" />
          <polygon points="9.75 15.02 15.5 11.75 9.75 8.48 9.75 15.02" fill="currentColor" />
        </svg>
      </a>
      <a
        href="https://www.linkedin.com/"
        target="_blank"
        rel="noopener noreferrer"
        aria-label="Connect on LinkedIn"
      >
        <svg
          class="social-icon"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z" />
          <rect x="2" y="9" width="4" height="12" />
          <circle cx="4" cy="4" r="2" />
        </svg>
      </a>
    </div>

    <!-- Right: Built on ClassroomIO -->
    <div class="flex flex-1 justify-end">
      <a
        href="https://classroomio.com"
        target="_blank"
        rel="noopener noreferrer"
        class="footer-built-on flex items-center gap-1"
      >
        <p class="footer-built-on-text text-base font-semibold text-[#22113E] underline">
          Built on ClassroomIO
        </p>
      </a>
    </div>
  </nav>
{/if}

<style>
  .footer-built-on-text {
    font-family: 'Space Grotesk', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI',
      sans-serif;
  }

  .social-icon {
    color: #22113e; /* deep purple */
    transition: color 150ms ease;
  }

  .social-icons a:hover .social-icon,
  .social-icons a:focus-visible .social-icon {
    color: #ea7dff; /* pink accent */
  }
</style>
