<!-- https://github.com/sveltejs/svelte-virtual-list -->

<script>
  import VirtualList from "./VirtualList.svelte";
  import items from "./data.js";
  import ListItem from "./ListItem.svelte";

  let searchTerm = "";

  $: filteredList = items.filter(
    (item) => item.Name.indexOf(searchTerm) !== -1
  );

  let start;
  let end;
</script>

<h1>Virtual list</h1>
<p>
  Instead of rendering all your data, &lt;VirtualList&gt; just renders the bits
  that are visible, keeping your page nice and light.
</p>
<p>
  The source code for the component is <a
    href="https://github.com/sveltejs/svelte-virtual-list">here</a
  >.
</p>

Filter:<input bind:value={searchTerm} />
{searchTerm}

<div class="container">
  <VirtualList items={filteredList} bind:start bind:end let:item>
    <ListItem {...item} />
  </VirtualList>
  <p>showing items {start}-{end}</p>
</div>

<style>
  .container {
    border-top: 1px solid #333;
    border-bottom: 1px solid #333;
    min-height: 200px;
    height: calc(100vh - 15em);
  }
</style>
