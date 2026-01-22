<script lang="ts">
  interface Props {
    description?: string;
    name?: string;
    banner?: string;
  }

  let { description = '', name = '', banner = '' }: Props = $props();
</script>

<section
  class="relative flex w-full max-w-[400px] flex-col justify-between space-y-4 rounded border border-[#EAEAEA] bg-[#FDFDFD] px-6 pt-4 pb-3 xl:max-w-[500px]"
>
  <img src="/quote.svg" alt="" class="absolute left-8 top-4 h-6 w-6 rounded-full" />
  <div>
    <p class="my-3 line-clamp-5 font-bold">
      {description}
    </p>
  </div>
  <div class="flex items-center gap-4 border-t border-[#EAEAEA] p-3">
    <img src={banner ? banner : '/course-banner.jpg'} alt="" class="h-6 w-6 rounded-full" />
    <span>
      <p class="text-sm font-bold">{name}</p>
    </span>
  </div>
</section>
