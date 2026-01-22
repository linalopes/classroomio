<script lang="ts">
  import { cn } from '$lib/utils';

  interface Props {
    onClick?: () => void;
    label: string;
    href?: string | undefined;
    class?: string | undefined;
    children?: any;
  }
  const { onClick, children, label, href, class: className, ...restProps }: Props = $props();
</script>

{#if href}
  <a
  {href}
    class={cn('classic-primary-btn', className)}
  onclick={onClick}
  {...restProps}
>
    {#if label}
      {label}
    {:else}
      {@render children?.()}
    {/if}
  </a>
{:else}
  <button
    class={cn('classic-primary-btn', className)}
    onclick={onClick}
    type="button"
    {...restProps}
  >
    {#if label}
  {label}
    {:else}
    {@render children?.()}
  {/if}
  </button>
{/if}
