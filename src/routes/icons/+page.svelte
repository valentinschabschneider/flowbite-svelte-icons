<script>
  import Label from 'flowbite-svelte/Label.svelte';
  import Range from 'flowbite-svelte/Range.svelte';
  import Tabs from 'flowbite-svelte/Tabs.svelte';
  import TabItem from 'flowbite-svelte/TabItem.svelte';
  import TableSearch from 'flowbite-svelte/TableSearch.svelte';
  import Icon from '$lib/Icon.svelte';
  import icons from '$lib/icons.js';
  import { random_tailwind_color, random_hex_color_code} from '../utils.js'

  const contentClass = 'rounded-lg dark:bg-neutral-900 mt-4';
  let searchTerm = '';

  $: filteredIconNames = Object.keys(icons).filter(name => {
    return name.toLowerCase().indexOf(searchTerm.toLowerCase()) !== -1;
  });
  let size="6"
</script>
<h1>Flowbite Svelte Icons: Icons</h1>
<TableSearch
  placeholder="Search by icon name"
  hoverable={true}
  bind:inputValue={searchTerm}
  divClass='relative overflow-x-auto'
>
<div class="lg:w-1/5 md:w-1/4 sm:w-1/3 w-full p-4">
  <Label class="text-lg py-4 ">Icon size: {size}</Label>
  <Range id="range1" min="4" max="10" step="2" bind:value={size} />
</div>
  <Tabs style="pill" {contentClass} class="p-4">
    <TabItem open>
      <span slot="title" class="text-lg">Mono</span>
      <div class="grid xl:grid-cols-5 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2 grid-cols-1 gap-8 px-4 dark:text-white">
        {#each filteredIconNames as iconName, i}
        <div class="flex gap-4 items-center text-lg">
          <svelte:component this={Icon} name={iconName} class="shrink-0 h-{size} w-{size}" />
          {iconName}
        </div>
        {/each}
      </div>
    </TabItem>
    <TabItem>
      <span slot="title" class="text-lg">Random Hex Colors</span>
      <div class="grid xl:grid-cols-5 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2 grid-cols-1 gap-8 px-4 dark:text-white">
        {#each filteredIconNames as iconName, i}
        <div class="flex gap-4 items-center text-lg">
          <svelte:component
          this={Icon}
          name={iconName}
          color={random_hex_color_code()}
          class="shrink-0 h-{size} w-{size}"
        />
        {iconName}
        </div>
        {/each}
      </div>
    </TabItem>
    <TabItem>
      <span slot="title" class="text-lg">Random Tailwind CSS Colors</span>
      <div class="grid xl:grid-cols-5 lg:grid-cols-4 md:grid-cols-3 sm:grid-cols-2 grid-cols-1 gap-8 px-4 dark:text-white">
        {#each filteredIconNames as iconName, i}
        <div class="flex gap-4 items-center text-lg">
          <svelte:component this={Icon} name={iconName} class="{random_tailwind_color()} shrink-0 h-{size} w-{size}" />
          {iconName}
        </div>
        {/each}
      </div>
    </TabItem>
  </Tabs>
</TableSearch>
