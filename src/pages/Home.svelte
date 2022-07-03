<script>
  import { Button, Card, CardBody } from 'sveltestrap'
  import TopNavbar from '../components/TopNavbar.svelte'
  export let notebooks = []
</script>

<TopNavbar />

<div class="container py-3 text-break">
  <h1>Home</h1>
  <Card style="cursor: pointer;" on:click={() => location.hash = "#/book/"}>
    <CardBody>
      <lottie-player src="https://assets9.lottiefiles.com/packages/lf20_kq5rGs.json"  background="transparent"  speed="1"  style="width: 100%; height: 300px;"  loop autoplay></lottie-player>
      <h2>Books</h2>
    </CardBody>
  </Card>
  <Card style="cursor: pointer;" on:click={() => location.hash = "#/additem/"}>
    <CardBody>
      <lottie-player src="https://assets9.lottiefiles.com/packages/lf20_gfpgyvtn.json"  background="transparent"  speed="1"  style="width: 100%; height: 300px;"  loop autoplay></lottie-player>
      <h2>Add Item To Book</h2>
    </CardBody>
  </Card>
  <Button color="primary" on:click={() => location.hash = "#/addbook/"}>
    <i class="fa-solid fa-circle-plus"></i>
    Add A New Book
  </Button>
  <Button color="primary" on:click={() => location.hash = "#/additem/"}>
    <i class="fa-solid fa-circle-plus"></i>
    Add Item To Book
  </Button>
  <Button color="primary" on:click={() => location.hash = "#/editbook/"}>
    <i class="fa-solid fa-pen-to-square"></i>
    Edit Books
  </Button>
</div>