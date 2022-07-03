<script>
  import { Offcanvas, Nav, NavItem, NavLink } from 'sveltestrap'
  export let open
  export let toggleOffcanvas
</script>

<Offcanvas isOpen={open} toggle={toggleOffcanvas} header="Chineseoo" placement="end">
  <Nav navbar >
    <NavItem>
      <NavLink href="#/">Home</NavLink>
    </NavItem>
    <NavItem>
      <NavLink active href="#/book/">Books</NavLink>
    </NavItem>
  </Nav>
</Offcanvas>