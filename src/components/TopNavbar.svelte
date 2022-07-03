<script>
  import OffcanvasNav from '../components/OffcanvasNav.svelte'
  import { Navbar, NavbarBrand, NavbarToggler } from 'sveltestrap'
  let open = false
  const toggleOffcanvas = () => (open = !open)
</script>

<Navbar color="light" light>
  <NavbarBrand href="#/" class="me-auto">Chineseoo</NavbarBrand>
  <NavbarToggler on:click={toggleOffcanvas} class="me-2" />
  <OffcanvasNav {open} {toggleOffcanvas} />
</Navbar>
