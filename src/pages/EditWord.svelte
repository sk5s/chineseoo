<script>
  import EditableWordsList from "../components/EditableWordsList.svelte"
  import TopNavbar from "../components/TopNavbar.svelte"
  import { Breadcrumb, BreadcrumbItem } from "sveltestrap"
  export let notebooks = []
  export let hashParam = ""
</script>

<TopNavbar />

<div class="container py-3 text-break">
  <Breadcrumb>
    <BreadcrumbItem>
      <a href="#/">Home</a>
    </BreadcrumbItem>
    <BreadcrumbItem>
      Edit Word
    </BreadcrumbItem>
  </Breadcrumb>

  <EditableWordsList bind:hashParam bind:notebooks on:chineseoo_delete_a_word on:chineseoo_move_one_word_up />
</div>