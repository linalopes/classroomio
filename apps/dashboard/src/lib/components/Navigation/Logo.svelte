<script lang="ts">
  import { t } from '$lib/utils/functions/translations';

  export let logo: string | undefined;
  export let orgName: string | undefined;
</script>

<div class="logo">
  <a
    href="/"
    title={`${$t('navigation.goto')} ${orgName || 'School of Tomorrows AI'} ${$t('navigation.home')}`}
    class="flex items-center gap-2"
    id="logo"
    data-hveid="8"
  >
    <img
      src={logo || '/logo.svg'}
      alt={`${orgName || 'School of Tomorrows AI'} logo`}
      class="mx-auto inline-block w-9 rounded"
      data-atf="1"
    />
    {#if orgName}
      <span class="line-clamp-1 hidden text-sm font-medium md:block">{orgName}</span>
    {/if}
  </a>
</div>
