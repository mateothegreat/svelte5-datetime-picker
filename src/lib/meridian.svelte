<script lang="ts">
  import { Select } from "bits-ui";
  import type { Writable } from "svelte/store";

  type Props = {
    value: Writable<string>;
  };

  let { value }: Props = $props();
</script>

{#snippet item(v: string)}
  <Select.Item class="data-[highlighted]:bg-muted select-none rounded px-2 py-1 text-xs outline-none duration-75" value={v}>
    {v}
  </Select.Item>
{/snippet}

<Select.Root type="single" onValueChange={(v) => ($value = v)}>
  <Select.Trigger
    class="bg-background placeholder:text-foreground-alt/50 inline-flex h-8 select-none items-center gap-1 rounded border px-2 text-center text-xs transition-colors"
    aria-label="Select">
    {$value}
    <svg class="h-4 w-4" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 256 256">
      <g fill="currentColor">
        <path d="M80 176h96l-48 48Zm48-144L80 80h96Z" opacity="0.2" />
        <path
          d="M176 168H80a8 8 0 0 0-5.66 13.66l48 48a8 8 0 0 0 11.32 0l48-48A8 8 0 0 0 176 168m-48 44.69L99.31 184h57.38ZM80 88h96a8 8 0 0 0 5.66-13.66l-48-48a8 8 0 0 0-11.32 0l-48 48A8 8 0 0 0 80 88m48-44.69L156.69 72H99.31Z" />
      </g>
    </svg>
  </Select.Trigger>
  <Select.Portal>
    <Select.Content
      class="focus-override border-muted bg-background shadow-popover data-[state=open]:animate-in data-[state=closed]:animate-out data-[state=closed]:fade-out-0 data-[state=open]:fade-in-0 data-[state=closed]:zoom-out-95 data-[state=open]:zoom-in-95 data-[side=bottom]:slide-in-from-top-2 data-[side=left]:slide-in-from-right-2 data-[side=right]:slide-in-from-left-2 data-[side=top]:slide-in-from-bottom-2 z-50 max-h-96  select-none rounded border py-1 outline-none data-[side=bottom]:translate-y-1 data-[side=left]:-translate-x-1 data-[side=right]:translate-x-1 data-[side=top]:-translate-y-1">
      <Select.Viewport class="px-2 py-1">
        {@render item("AM")}
        {@render item("PM")}
      </Select.Viewport>
    </Select.Content>
  </Select.Portal>
</Select.Root>
