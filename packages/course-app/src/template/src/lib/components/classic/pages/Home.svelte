<script lang="ts">
  import { getPageSection } from '@/utils/helpers/page';
  import { homePage } from '@/utils/stores/pages';
  import PrimaryButton from '../PrimaryButton.svelte';
  import { goto } from '$app/navigation';
  import patternImage from '../assets/LiloAcademy_Pattern_1.png';
  import { courses } from '@/utils/stores/course';
  import CourseCard from '../CourseCard.svelte';
  import EmptyState from '../EmptyState.svelte';
  import InstructorCard from '../InstructorsCard.svelte';
  import Accordion from '../Accordion.svelte';
  import TestimonialCard from '../TestimonialCard.svelte';
  import BlogCard from '../BlogCard.svelte';
  import { SECTION } from '@/utils/constants/page';

  const faqSection = $derived(getPageSection($homePage, SECTION.FAQ));
  const testimonialSection = $derived(getPageSection($homePage, SECTION.TESTIMONIAL));
  const aboutSection = $derived(getPageSection($homePage, SECTION.ABOUT));
  const courseSection = $derived(getPageSection($homePage, SECTION.COURSE));
  const instructorSection = $derived(getPageSection($homePage, SECTION.INSTRUCTORS));
  const ctaSection = $derived(getPageSection($homePage, SECTION.CTA));

  let viewAll = $state(false);
</script>

<main>
  <!-- School of Tomorrow's AI 2026 Hero -->
  <section
    id="hero"
    class="hero-section relative bg-white"
    style="background-image: url('{patternImage}');"
  >
    <div class="hero-overlay"></div>
    <div
      class="hero-content relative z-10 mx-auto max-w-4xl px-4 py-16 text-center sm:px-6 sm:py-20 lg:px-8 lg:py-24"
    >
      <!-- Eyebrow / Label -->
      <p class="mb-6 font-mono text-sm uppercase tracking-wide text-[#22113E]">
        ART AND CREATIVE TECHNOLOGY SCHOOL · 2026 PROGRAM
      </p>

      <!-- Main Heading -->
      <h1
        class="font-heading mb-6 text-4xl font-light leading-tight text-[#22113E] sm:text-5xl lg:text-6xl"
      >
        Room for Interaction
      </h1>

      <!-- Supporting Line -->
      <p class="font-heading mb-8 text-xl font-light text-[#22113E] sm:text-2xl lg:text-3xl">
        A playground for body, space and technology.
      </p>

      <!-- Body Copy -->
      <p
        class="mx-auto mb-8 max-w-2xl text-base leading-relaxed text-[#22113E] sm:text-lg lg:text-xl"
      >
        School of Tomorrow's AI is a creative art & technology school. In 2026 we are running a
        program of seven hands-on workshops under the umbrella <em class="font-semibold"
          >Room for Interaction</em
        > — a series where you choreograph movement, light, sensors and AI in playful, guided experiments.
        An initiative of the School of Tomorrows AI in collaboration with Glitch Lab.
      </p>

      <!-- CTA Buttons -->
      <div class="mt-8 flex flex-col items-center justify-center gap-4 sm:flex-row">
        <PrimaryButton href="/courses" label="Browse courses" />
        <a href="/courses" class="hero-secondary-btn"> View Augmented Cinema </a>
      </div>
    </div>
  </section>

  <hr class="border-classic-border mb-10 mt-5" />

  <!-- about -->

  {#if aboutSection?.show}
    <section
      id="about"
      class="flex h-full items-start justify-center border-b-2 bg-white px-6 pb-20 pt-4 md:px-10 lg:px-14 lg:pt-20"
    >
      <section class="flex flex-col items-center justify-center gap-4 lg:flex-row lg:items-start">
        <div class="w-full space-y-4 lg:w-[60%]">
          <p class="text-4xl font-bold text-[#3F3F3F]">{aboutSection.settings.title}</p>
          <p class="w-full text-base leading-7 text-[#878787] lg:w-[80%]">
            {aboutSection.settings.content}
          </p>
        </div>
        {#if aboutSection.settings.benefits}
          <div class="min-h-fit w-full max-w-[520px]">
            <div class="grid grid-cols-1 gap-6 md:grid-cols-2">
              {#each aboutSection.settings.benefits.list as item}
                <div
                  class="benefit-card rounded-b-lg border-b-4 border-[#EA7DFF] bg-white px-5 py-4 text-center font-semibold shadow-lg"
                >
                  {item.title}
                </div>
              {/each}
            </div>
          </div>
        {:else}
          <img
            src={aboutSection.settings.imageUrl}
            alt="Our Story"
            class="max-h-[450px] rounded-2xl"
          />
        {/if}
      </section>
    </section>
  {/if}

  <!-- courses -->
  {#if courseSection?.show}
    <section id="course" class="h-full bg-white px-4 py-6 pb-20">
      <h1 class="mb-4 text-center text-3xl font-bold text-[#3F3F3F]">
        {courseSection.settings.title}
      </h1>
      <div class="mx-auto w-full md:w-[90%]">
        {#if $courses.length > 0}
          <section class="mx-auto flex w-fit flex-wrap items-center gap-4">
            {#each $courses.slice(0, viewAll ? $courses.length : 3) as courseData}
              <CourseCard
                slug={courseData.slug}
                bannerImage={courseData.banner || '/course-banner.jpg'}
                title={courseData.title}
                type={courseData.type}
                description={courseData.description}
                cost={courseData.cost}
                currency={courseData.currency}
                totalLessons={courseData.lessonsCount}
              />
            {/each}
          </section>
          {#if $courses.length > 3}
            <div class="my-5 flex w-full items-center justify-center">
              <PrimaryButton
                class="bg-[#EA7DFF] text-lg font-semibold text-white"
                onClick={() => (viewAll = !viewAll)}
                label="View more programs"
              />
            </div>
          {/if}
        {:else}
          <div class="mx-auto w-full px-4 lg:w-[70%]">
            <EmptyState headerClassName="text-[#EA7DFF]" />
          </div>
        {/if}
      </div>
    </section>
  {/if}
  <!-- instructors -->
  {#if instructorSection?.show}
    <section class="h-full bg-white px-4 pb-20 pt-4 lg:px-14">
      <div class="mx-auto w-full xl:w-[90%]">
        <h1 class=" mb-4 text-center text-3xl font-bold text-[#3F3F3F] lg:text-start">
          Meet some of our Instructors
        </h1>
        <section class="grid w-full grid-cols-1 place-items-center gap-2 md:grid-cols-2">
          {#each instructorSection.settings.list as item}
            <InstructorCard name={item.name} description={item.description} rating={item.rating} />
          {/each}
        </section>
        <div class="mt-6 flex w-full justify-center px-4 md:justify-end">
          <PrimaryButton
            class="rounded p-6 text-lg font-semibold text-white"
            label="Start learning & Explore courses"
          />
        </div>
      </div>
    </section>
  {/if}
  <!-- faq -->
  {#if faqSection?.show}
    <section class="h-full bg-[#F9F9F9] px-4 py-6 pb-20">
      <h1 class="mb-4 text-center text-3xl font-bold text-[#3F3F3F]">
        {faqSection.settings.title}
      </h1>
      <section class="mx-auto w-full space-y-10 p-2 md:w-[80%]">
        {#each faqSection.settings.questions as faq}
          <Accordion title={faq.title} content={faq.content} />
        {/each}
      </section>
    </section>
  {/if}
  <!-- testimonial -->
  {#if testimonialSection?.show}
    <section id="testimonial" class="h-full bg-white px-4 pb-20 pt-4 lg:px-14">
      <h1 class="mb-4 text-center text-3xl font-bold text-[#3F3F3F]">
        Words from our past learners
      </h1>
      <section class="grid w-full grid-cols-1 gap-4 md:grid-cols-2 xl:grid-cols-3">
        {#each testimonialSection.settings.list as item}
          <TestimonialCard description={item.description} name={item.name} />
        {/each}
      </section>
    </section>
  {/if}
  <!-- cta -->
  {#if ctaSection?.show}
    <section class="bg-classic flex flex-col items-center justify-between px-6 py-20 lg:px-10">
      <div class="flex w-full items-center justify-center">
        <p class="w-full text-center text-4xl font-bold text-white">
          {ctaSection.settings.title}
        </p>
      </div>
      <div class="my-5 flex w-full items-center justify-center">
        <PrimaryButton
          href={ctaSection.settings?.button?.link}
          class="bg-classic-secondary hover:bg-classic-secondary text-classic rounded-sm border border-gray-100 text-lg font-bold hover:scale-95"
          label={ctaSection.settings?.button?.label}
        />
      </div>
    </section>
  {/if}

  <!-- blog -->
  <section id="course" class="hidden h-full bg-white px-4 py-6 pb-20">
    <h1 class="mb-4 text-center text-3xl font-bold text-[#3F3F3F]">Latest blog Post</h1>
    <section class="mx-auto flex w-full flex-wrap items-center gap-2">
      <BlogCard />
      <BlogCard />
      <BlogCard />
      <BlogCard />
    </section>
  </section>
</main>

<style>
  .benefit-card {
    transition: transform 0.3s ease-in-out;
    position: relative;
  }
</style>
