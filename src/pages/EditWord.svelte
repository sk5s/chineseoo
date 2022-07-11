<script>
  import EditableWordsList from "../components/EditableWordsList.svelte"
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem } from "sveltestrap"
  export let notebooks = []
  export let hashParam = ""
  let notebook = notebooks.filter((item) => {
    return item.id == hashParam
  })
  notebook = notebook[0]
</script>

<TopNavbar />

<div class="container py-3 text-break">
  <Breadcrumb>
    <BreadcrumbItem>
      <a href="#/">Home</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      <a href="#/editword/">Edit Word</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      {notebook.name}
    </BreadcrumbItem>
  </Breadcrumb>

  <h1>Book: {notebook.name}</h1>

  <EditableWordsList bind:hashParam bind:notebooks on:chineseoo_delete_a_word on:chineseoo_move_one_word_up />
</div>