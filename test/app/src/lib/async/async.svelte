<script lang="ts">
  import { route, Router, type Route } from "@mateothegreat/svelte5-router";
  import { onMount } from "svelte";
  import Child from "./child.svelte";

  onMount(() => {
    console.log("child.svelte", "onMount");
  });

  const routes: Route[] = [
    {
      path: "child",
      component: Child
    }
  ];
</script>

<div class="flex flex-col gap-3 bg-gray-400 p-10">
  <p class="rounded-lg bg-black p-2 text-center text-xs text-green-500">a.svelte</p>
  <h1>Parent: AsyncFunction</h1>
  <div class="flex gap-2 rounded-lg bg-black p-4">
    <a use:route href="/async/child" class="rounded-lg bg-blue-500 px-2">/async/child</a>
  </div>
  <div class="rounded-lg bg-black p-4 shadow-xl">
    <Router {routes} />
  </div>
</div>
