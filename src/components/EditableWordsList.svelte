<script>
  import { ListGroup, ListGroupItem, Input, Nav, NavItem, Button, Alert, ButtonGroup } from 'sveltestrap'
  import CountText from './CountText.svelte'
  import { createEventDispatcher, onMount } from 'svelte'
  export let notebooks = []
  export let hashParam
  let notebook = notebooks.filter((item) => {
    return item.id == hashParam
  })
  notebook = notebook[0]
  console.log(notebook)
  $: count = notebook.data.length
  $: actionlist = []
  onMount(() => {
    notebook = notebooks.filter((item) => {
      return item.id == hashParam
    })
    notebook = notebook[0]
  })
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
      dispatch("chineseoo_delete_a_word", {
        wordId: text
      })
    })
    actionlist = []
    location.reload()
  }
  const viewWords = () => {
    location.hash = "#/book/"+hashParam
  }
  const moveUp = (oldIndex) => {
    console.log(oldIndex)
    dispatch("chineseoo_move_one_word_up", {
      itemIndex: oldIndex,
      bookId: hashParam
    })
    location.reload()
  }
</script>

<Nav class="justify-content-end">
  <NavItem>
    <ButtonGroup>
      <Button color="primary" on:click={viewWords} ><i class="fa-solid fa-eye"></i> View Words</Button>
      <Button color="primary" disabled={actionlist.length == 0} on:click={deleteSelection} ><i class="fa-solid fa-pen-to-square"></i> Delete</Button>
    </ButtonGroup>
  </NavItem>
</Nav>

<ListGroup>
{#each notebook.data as word, i}
  <ListGroupItem class="d-flex">
    <Input class="checkbox" id={word.id} type="checkbox" on:input={checkHandler} />
    <Button alt="Move Word Up" size="sm" color="light" disabled={i == 0} on:click={() => moveUp(i)}><i class="fa-solid fa-angle-up"></i></Button>
    <a href="#/editword/" rel="nofollow noopener noreferrer" class="fs-5">
      {word.text}
    </a>
    <span>
      {word.description}
    </span>
  </ListGroupItem>
{/each}
</ListGroup>

{#if count != 0}
  <CountText {count} />
{:else}
  <Alert color="warning">Add Words First</Alert>
{/if}