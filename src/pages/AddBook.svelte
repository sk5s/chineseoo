<script>
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem, Button, FormGroup, Input, Alert } from 'sveltestrap'
  import { createEventDispatcher } from "svelte"
  const dispatch = createEventDispatcher()
  export let notebooks = []
  let name_input = ""
  let valid_name = true
  let valid_pattern = /[^\w\s\u4E00-\u9FFF]/gi
  const addNewBookHandler = () => {
    if (name_input == "") return
    let notes = notebooks.filter((item) => {
      return item.name == name_input
    })
    if (notes.length == 0) {
      dispatch('chineseoo_add_new_book', {
        name_input
      })
      location.hash = "#/"
      name_input = ""
    }
  }
  const keydownHandler = (e) => {
    if (e.keyCode == 13 && !(name_input == "" || !valid_name)){
      addNewBookHandler()
    }
  }
  const handleInput = (e) => {
    valid_name = e.target.value.replace(valid_pattern, '_') == e.target.value
  }
</script>

<TopNavbar />

<div class="container py-3 text-break">
  <Breadcrumb>
    <BreadcrumbItem>
      <a href="#/">Home</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      Add Book
    </BreadcrumbItem>
  </Breadcrumb>

  <h1>Add A New Book</h1>
  <FormGroup floating label="Input Book Name">
    <Input on:keydown={keydownHandler} on:input={handleInput} bind:value={name_input} placeholder="Enter a value" />
  </FormGroup>
  <Button disabled={name_input == "" || !valid_name} color="primary" on:click={addNewBookHandler}>Add</Button>

  {#if !valid_name}
    <Alert color="warning" class="mt-3">
      Name cannot include some special character.<br>
      <Button color="warning" on:click={() => {name_input = name_input.replace(valid_pattern, '_');valid_name = true}}>Use _ to replace invalid characters.</Button>
    </Alert>
  {/if}
</div>