<script>
  import { ListGroup, ListGroupItem } from 'sveltestrap'
  import CountText from './CountText.svelte';
  export let notebook = {}
  console.log(notebook)
  let book_data = notebook.data
  $: count = book_data.length
</script>

<ListGroup>
{#each book_data as item}
  <ListGroupItem>
    <a href="#/book/" rel="nofollow noopener noreferrer" class="fs-5">
      {item.text}
    </a>
    <span>
      {item.description}
    </span>
  </ListGroupItem>
{/each}
</ListGroup>

{#if count != 0}
  <CountText {count} />
{/if}