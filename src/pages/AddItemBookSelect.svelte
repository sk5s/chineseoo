<script>
  import BookSelect from "../components/BookSelect.svelte"
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem } from "sveltestrap"
  export let notebooks = []
</script>

<TopNavbar />

<div class="container py-3 text-break">
  <Breadcrumb>
    <BreadcrumbItem>
      <a href="#/">Home</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      Add Item
    </BreadcrumbItem>
  </Breadcrumb>
  
  <h1>Add Item To Book</h1>
  <BookSelect {notebooks} redirect_path="#/additem/" />
</div>
