<script>
  import { ListGroup, ListGroupItem, Alert } from 'sveltestrap'
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
{:else}
  <Alert color="warning">Add Book First</Alert>
{/if}