<script>
  import { ListGroup, ListGroupItem } from 'sveltestrap'
  import CountText from './CountText.svelte'
  export let notebooks = []
  console.log(notebooks)
  $: count = notebooks.length
</script>

<ListGroup>
{#each notebooks as notebook}
  <ListGroupItem>
    <a href="#/book/{notebook.id}" rel="nofollow noopener noreferrer">
      {notebook.name}
    </a>
  </ListGroupItem>
{/each}
</ListGroup>

{#if count != 0}
  <CountText {count} />
{/if}