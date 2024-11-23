<script lang="ts">
  import { Button, RangeCalendar, type DateRange } from "bits-ui";
  import { writable, type Writable } from "svelte/store";
  import Meridian from "./meridian.svelte";

  type Props = {
    value: Writable<DateRange>;
  };

  let { value }: Props = $props();

  let meridianStart = writable<string>("AM");
  let meridianEnd = writable<string>("AM");
</script>

{#snippet input(v: { for: "start" | "end"; prop: "hour" | "minute"; value: number })}
  <input
    bind:value={$value[v.for][v.prop]}
    onchange={(e) => {
      $value[v.for][v.prop] = parseInt(e.target.value);
    }}
    class="border-input placeholder:text-muted-foreground focus-visible:ring-ring flex h-8 w-11 rounded-md border bg-transparent px-3 py-1 text-center text-xs shadow-sm transition-colors file:border-0 file:bg-transparent file:text-sm file:font-medium focus-visible:outline-none focus-visible:ring-1 disabled:cursor-not-allowed disabled:opacity-50" />
{/snippet}

<RangeCalendar.Root {value} weekdayFormat="short" numberOfMonths={2} fixedWeeks={true} class="">
  {#snippet children({ months, weekdays }: { months: any; weekdays: any })}
    <RangeCalendar.Header class="flex items-center justify-between">
      <RangeCalendar.PrevButton class="rounded-9px bg-background-alt hover:bg-muted active:scale-98 inline-flex size-10 items-center justify-center">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24">
          <g fill="none" fill-rule="evenodd">
            <path
              d="M24 0v24H0V0zM12.593 23.258l-.011.002l-.071.035l-.02.004l-.014-.004l-.071-.035q-.016-.005-.024.005l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427q-.004-.016-.017-.018m.265-.113l-.013.002l-.185.093l-.01.01l-.003.011l.018.43l.005.012l.008.007l.201.093q.019.005.029-.008l.004-.014l-.034-.614q-.005-.019-.02-.022m-.715.002a.02.02 0 0 0-.027.006l-.006.014l-.034.614q.001.018.017.024l.015-.002l.201-.093l.01-.008l.004-.011l.017-.43l-.003-.012l-.01-.01z" />
            <path
              fill="currentColor"
              d="M7.94 13.06a1.5 1.5 0 0 1 0-2.12l5.656-5.658a1.5 1.5 0 1 1 2.121 2.122L11.122 12l4.596 4.596a1.5 1.5 0 1 1-2.12 2.122l-5.66-5.658Z" />
          </g>
        </svg>
      </RangeCalendar.PrevButton>
      <RangeCalendar.Heading class="text-[15px] font-medium" />
      <RangeCalendar.NextButton class="rounded-9px bg-background-alt hover:bg-muted active:scale-98 inline-flex size-10 items-center justify-center">
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24">
          <g fill="none" fill-rule="evenodd">
            <path
              d="M24 0v24H0V0zM12.593 23.258l-.011.002l-.071.035l-.02.004l-.014-.004l-.071-.035q-.016-.005-.024.005l-.004.01l-.017.428l.005.02l.01.013l.104.074l.015.004l.012-.004l.104-.074l.012-.016l.004-.017l-.017-.427q-.004-.016-.017-.018m.265-.113l-.013.002l-.185.093l-.01.01l-.003.011l.018.43l.005.012l.008.007l.201.093q.019.005.029-.008l.004-.014l-.034-.614q-.005-.019-.02-.022m-.715.002a.02.02 0 0 0-.027.006l-.006.014l-.034.614q.001.018.017.024l.015-.002l.201-.093l.01-.008l.004-.011l.017-.43l-.003-.012l-.01-.01z" />
            <path
              fill="currentColor"
              d="M16.06 10.94a1.5 1.5 0 0 1 0 2.12l-5.656 5.658a1.5 1.5 0 1 1-2.121-2.122L12.879 12L8.283 7.404a1.5 1.5 0 0 1 2.12-2.122l5.658 5.657Z" />
          </g>
        </svg>
      </RangeCalendar.NextButton>
    </RangeCalendar.Header>
    <div class="flex flex-col space-y-4 pt-4 sm:flex-row sm:space-x-4 sm:space-y-0">
      {#each months as month}
        <RangeCalendar.Grid class="w-full border-collapse select-none space-y-1">
          <RangeCalendar.GridHead>
            <RangeCalendar.GridRow class="mb-1 flex w-full justify-between">
              {#each weekdays as day}
                <RangeCalendar.HeadCell class="text-muted-foreground w-10 rounded-md text-xs !font-normal">
                  <div>{day.slice(0, 2)}</div>
                </RangeCalendar.HeadCell>
              {/each}
            </RangeCalendar.GridRow>
          </RangeCalendar.GridHead>
          <RangeCalendar.GridBody>
            {#each month.weeks as weekDates}
              <RangeCalendar.GridRow class="flex w-full">
                {#each weekDates as date}
                  <RangeCalendar.Cell {date} month={month.value} class="relative m-0 size-10 !p-0 text-center text-sm focus-within:z-20">
                    <RangeCalendar.Day
                      class="rounded-9px bg-background text-foreground hover:border-foreground focus-visible:!ring-foreground data-[selection-end]:rounded-9px data-[selection-start]:rounded-9px data-[highlighted]:bg-muted data-[selected]:bg-muted data-[selection-end]:bg-foreground data-[selection-start]:bg-foreground data-[disabled]:text-foreground/30 data-[selected]:text-foreground data-[selection-end]:text-background data-[selection-start]:text-background data-[unavailable]:text-muted-foreground data-[selected]:[&:not([data-selection-start])]:[&:not([data-selection-end])]:focus-visible:border-foreground group relative inline-flex size-10 items-center justify-center overflow-visible whitespace-nowrap border border-transparent bg-transparent p-0 text-sm font-normal data-[disabled]:pointer-events-none data-[outside-month]:pointer-events-none data-[highlighted]:rounded-none data-[selected]:font-medium data-[selection-end]:font-medium data-[selection-start]:font-medium data-[unavailable]:line-through data-[selection-start]:focus-visible:ring-2 data-[selection-start]:focus-visible:!ring-offset-2 data-[selected]:[&:not([data-selection-start])]:[&:not([data-selection-end])]:rounded-none data-[selected]:[&:not([data-selection-start])]:[&:not([data-selection-end])]:focus-visible:!ring-0 data-[selected]:[&:not([data-selection-start])]:[&:not([data-selection-end])]:focus-visible:!ring-offset-0">
                      <div
                        class="bg-foreground group-data-[selected]:bg-background absolute top-[5px] hidden size-1 rounded-full group-data-[today]:block">
                      </div>
                      {date.day}
                    </RangeCalendar.Day>
                  </RangeCalendar.Cell>
                {/each}
              </RangeCalendar.GridRow>
            {/each}
          </RangeCalendar.GridBody>
        </RangeCalendar.Grid>
      {/each}
    </div>
    <div class="mt-2 flex w-full items-center justify-between">
      <div class="flex items-center gap-1 text-xs text-slate-400">
        Time:
        {@render input({ for: "start", prop: "hour", value: $value.start.hour })}
        <span class="text-slate-500">:</span>
        {@render input({ for: "start", prop: "minute", value: $value.start.minute })}
        <span class="text-slate-500">:</span>
        {@render input({ for: "start", prop: "second", value: $value.start.second })}
        <Meridian value={meridianStart} />
        <span class="text-slate-500">-</span>
        {@render input({ for: "end", prop: "hour", value: $value.end.hour })}
        <span class="text-slate-500">:</span>
        {@render input({ for: "end", prop: "minute", value: $value.end.minute })}
        <span class="text-slate-500">:</span>
        {@render input({ for: "end", prop: "second", value: $value.end.second })}
        <Meridian value={meridianEnd} />
      </div>
      <div class="text-muted-foreground text-sm">
        <Button.Root
          class="hover:bg-dark/95 inline-flex h-8 items-center justify-center px-[21px] text-xs font-semibold text-slate-500 active:scale-95 active:transition-all">
          Cancel
        </Button.Root>
        <Button.Root
          class="hover:bg-dark/95 inline-flex h-8 items-center justify-center rounded border border-slate-800 px-[21px] text-xs font-semibold active:scale-95 active:transition-all dark:text-white">
          Apply
        </Button.Root>
      </div>
    </div>
  {/snippet}
</RangeCalendar.Root>
