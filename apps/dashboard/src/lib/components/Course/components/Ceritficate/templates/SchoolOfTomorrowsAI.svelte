<script>
  import { course } from '$lib/components/Course/store';
  import { currentOrg } from '$lib/utils/store/org';

  export let studentName = '';
  const logo = '/logo.svg';
</script>

<!-- Root container with background pattern -->
<div class="certificate-root relative w-full border border-[#22113E] bg-white">
  <!-- Background pattern image -->
  <img
    src="/LiloAcademy_Pattern_2.png"
    alt=""
    aria-hidden="true"
    class="pattern-overlay pointer-events-none absolute inset-0 opacity-10"
  />

  <!-- Content wrapper with higher z-index -->
  <div class="relative z-10 flex w-full items-center justify-center">
    <div class="w-full px-5 py-3">
      <!-- Certificate header -->
      <p
        class="certificate-header my-4 text-center text-xs font-normal uppercase tracking-widest text-[#22113E]"
      >
        Certificate of completion
      </p>

      <!-- Main certification statement -->
      <div class="mb-6 border-b-2 border-[#ea7dff] pb-4">
        <p class="mb-2 text-center text-sm font-normal text-[#22113E]">This is to certify that</p>
        <p class="student-name text-center text-5xl font-bold text-[#22113E]">{studentName}</p>
      </div>

      <!-- Course completion details -->
      <div class="mb-4">
        <p class="mb-3 text-center text-sm font-normal text-[#22113E]">
          has successfully completed introductory courses in
        </p>
        <p
          class="course-title mb-4 text-center text-lg font-semibold uppercase tracking-wide text-[#22113E]"
        >
          {$course.title}
        </p>
      </div>

      <!-- Description -->
      <p class="desc mb-6 text-justify text-sm leading-relaxed text-[#22113E]">
        {$course.description}
      </p>

      <!-- Footer with logo and organization name -->
      <div class="mt-8 flex items-center justify-center gap-2 border-t border-[#22113E] pt-4">
        <img
          src={$currentOrg.avatar_url ? $currentOrg.avatar_url : logo}
          alt="Organization logo"
          class="h-10 w-10 rounded-md"
        />
        <p class="font-semibold text-[#22113E]">School of Tomorrow's AI</p>
      </div>
    </div>
  </div>
</div>

<style>
  .certificate-root {
    min-height: 400px;
  }

  .pattern-overlay {
    object-fit: cover;
    object-position: center;
  }

  .certificate-header {
    letter-spacing: 0.15em;
  }

  .student-name {
    font-family:
      'Inter',
      system-ui,
      -apple-system,
      BlinkMacSystemFont,
      'Segoe UI',
      sans-serif;
    font-weight: 700;
    line-height: 1.2;
  }

  .course-title {
    letter-spacing: 0.1em;
  }

  .desc {
    font-size: 0.875rem;
    line-height: 1.6;
  }
</style>
