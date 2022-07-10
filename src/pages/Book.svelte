<script>
  import WordsList from "../components/WordsList.svelte"
  import NotFound from "./NotFound.svelte"
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem, Button, Nav, NavItem, ButtonGroup } from 'sveltestrap'
  export let hashParam = ""
  export let notebooks = []
  let notebook = notebooks.filter((item) => {
    return item.id == hashParam
  })
  notebook = notebook[0]
  const addWord = () => {
    location.hash = `#/additem/${hashParam}`
  }
  const editWord = () => {
    location.hash = `#/editword/${hashParam}`
  }
</script>

{#if notebook}

<TopNavbar />

<div class="container py-3 text-break">

  <Breadcrumb>
    <BreadcrumbItem>
      <a href="#/">Home</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      <a href="#/book/">Book</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      {notebook.name}
    </BreadcrumbItem>
  </Breadcrumb>

  <h1>Book: {notebook.name}</h1>

  <Nav class="justify-content-end">
    <NavItem>
      <ButtonGroup>
        <Button color="primary" on:click={editWord} ><i class="fa-solid fa-pen-to-square"></i> Edit</Button>
        <Button color="primary" on:click={addWord} ><i class="fa-solid fa-circle-plus"></i> Add Item</Button>
      </ButtonGroup>
    </NavItem>
  </Nav>

  <WordsList bind:notebook />

</div>

{:else}
  <NotFound />
{/if}

