<script lang="ts">
  import { CalendarDateTime } from "@internationalized/date";
  import { DateTimePicker } from "@mateothegreat/svelte5-datetime-picker";
  import type { DateRange } from "bits-ui";
  import { writable } from "svelte/store";

  const defaultDate = new Date();

  let value = writable<DateRange>({
    start: new CalendarDateTime(
      defaultDate.getFullYear(),
      defaultDate.getMonth() + 1,
      defaultDate.getDate(),
      defaultDate.getHours() - 1,
      defaultDate.getMinutes(),
      defaultDate.getSeconds()
    ),
    end: new CalendarDateTime(
      defaultDate.getFullYear(),
      defaultDate.getMonth() + 1,
      defaultDate.getDate(),
      defaultDate.getHours(),
      defaultDate.getMinutes(),
      defaultDate.getSeconds(),
      defaultDate.getMilliseconds()
    )
  });
</script>

<div class="absolute flex h-full w-full flex-col items-center gap-4 bg-black">
  <div class="flex w-full items-center justify-between p-6">
    <h1 class="font-mono text-lg text-indigo-500">
      <div class="flex flex-col items-center gap-2">
        Svelte 5 DateTimePicker Demo
        <div class="flex items-center gap-1">
          <pre class="text-xs text-slate-500">{JSON.stringify($value, null, 2)}</pre>
        </div>
      </div>
    </h1>
    <div class="border-dark-10 bg-background-alt shadow-card mt-6 rounded-lg border p-[22px]">
      <DateTimePicker {value} />
    </div>
  </div>
</div>
