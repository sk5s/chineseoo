<script>
  import EditableNoteBooksList from "../components/EditableNoteBooksList.svelte"
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
      Edit Books
    </BreadcrumbItem>
  </Breadcrumb>

  <EditableNoteBooksList {notebooks} on:chineseoo_delete_a_book />
</div>