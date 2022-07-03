<script>
  import WordsList from "../components/WordsList.svelte"
  import NotFound from "./NotFound.svelte"
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem } from 'sveltestrap'
  export let hashParam = ""
  export let notebooks = []
  let notebook = notebooks.filter((item) => {
    return item.id == hashParam
  })
  notebook = notebook[0]
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
  <WordsList {notebook} />

</div>

{:else}
  <NotFound />
{/if}

