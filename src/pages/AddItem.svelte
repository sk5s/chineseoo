<script>
  import NotFound from "./NotFound.svelte"
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem, FormGroup, Input, Button, Alert } from 'sveltestrap'
  import { createEventDispatcher } from "svelte"
  export let hashParam = ""
  export let notebooks = []
  const dispatch = createEventDispatcher()
  let notebook = notebooks.filter((item) => {
    return item.id == hashParam
  })
  notebook = notebook[0]
  let name_input = ""
  let content_input = ""
  let valid_name = true
  let valid_content = true
  let valid_pattern = /[^\w\s\u4E00-\u9FFF]/gi
  const addNewItemHandler = () => {
    if (name_input == "" || content_input == "") return
    let notes = []
    console.log(notebook)
    if (notebook.data.length != 0){
      notes = notebook.data.filter((item) => {
        return item.name == name_input
      })
    }
    if (notes.length == 0) {
      dispatch('chineseoo_add_new_word', {
        hashParam,
        name_input,
        content_input
      })
      location.hash = "#/book/"+hashParam
      name_input = ""
      content_input = ""
    }
  }
  const handleNameInput = (e) => {
    // valid_name = e.target.value.replace(valid_pattern, '_') == e.target.value
  }
  const handleContentInput = (e) => {
    // valid_content = e.target.value.replace(valid_pattern, '_') == e.target.value
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
      <a href="#/additem/">Add Item</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      {notebook.name}
    </BreadcrumbItem>
  </Breadcrumb>

  <h1>Add Item To Book: {notebook.name}</h1>
  <FormGroup floating label="Input Item Name">
    <Input on:input={handleNameInput} bind:value={name_input} placeholder="Enter a value" />
  </FormGroup>
  <FormGroup floating label="Input Item Content">
    <Input type="textarea" style="height: 100px" on:input={handleContentInput} bind:value={content_input} placeholder="Enter a value" />
  </FormGroup>
  <Button disabled={name_input == "" || content_input == "" || !valid_name || !valid_content} color="primary" on:click={addNewItemHandler}>Add</Button>

  {#if !valid_name || !valid_content}
    <Alert color="warning" class="mt-3">
      Name cannot include some special character.<br>
      <Button color="warning" on:click={() => {name_input = name_input.replace(valid_pattern, '_');content_input = name_input.replace(content_input, '_');valid_name = true;valid_content=true}}>Use _ to replace invalid characters.</Button>
    </Alert>
  {/if}
</div>

{:else}
  <NotFound />
{/if}