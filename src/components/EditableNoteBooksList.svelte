<script>
  import { ListGroup, ListGroupItem, Input, Nav, NavItem, Button, Alert, ButtonGroup } from 'sveltestrap'
  import CountText from './CountText.svelte'
  import { createEventDispatcher } from 'svelte'
  export let notebooks = []
  console.log(notebooks)
  $: count = notebooks.length
  $: actionlist = []
  const checkHandler = (e) => {
    console.log(e.target.id, e.target.checked)
    if (e.target.checked){
      actionlist = [...actionlist, e.target.id]
    } else {
      actionlist = actionlist.filter((id) => {
        return id != e.target.id
      })
    }
    console.log(actionlist, actionlist.length == 0)
  }
  const dispatch = createEventDispatcher()
  const deleteSelection = () => {
    actionlist.forEach((text) => {
      console.log(text)
      dispatch("chineseoo_delete_a_book", {
        bookId: text
      })
    })
    actionlist = []
    // location.reload()
  }
  const viewBooks = () => {
    location.hash = "#/book/"
  }
</script>

<Nav class="justify-content-end">
  <NavItem>
    <ButtonGroup>
      <Button color="primary" on:click={viewBooks} ><i class="fa-solid fa-eye"></i> View Books</Button>
      <Button color="primary" disabled={actionlist.length == 0} on:click={deleteSelection} ><i class="fa-solid fa-pen-to-square"></i> Delete</Button>
    </ButtonGroup>
  </NavItem>
</Nav>

<ListGroup>
{#each notebooks as notebook}
  <ListGroupItem class="d-flex">
    <Input class="checkbox" id={notebook.id} type="checkbox" on:input={checkHandler} />
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