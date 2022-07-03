<script>
  import NoteBooksList from '../components/NoteBooksList.svelte'
  import TopNavbar from '../components/TopNavbar.svelte'
  import { Breadcrumb, BreadcrumbItem } from 'sveltestrap'
  export let notebooks = []
</script>

<TopNavbar />

<div class="container py-3 text-break">

  <Breadcrumb>
    <BreadcrumbItem>
      <a href="#/">Home</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      Book
    </BreadcrumbItem>
  </Breadcrumb>

  <h1>Notebooks</h1>

  <NoteBooksList {notebooks} />

</div>