<script>
  import Customers from "./component/Customers.svelte";
  import CreateCustomer from "./component/CreateCustomer.svelte";
  import Home from "./component/Home.svelte";
  import { Router, Route } from "svelte-routing";
</script>

<ul id="menu">
  <li><a href="/home" component={Home} on:click>Home</a></li> |
	<li><a href="/customers" component={Customers} on:click>Customer</a></li> |
	<li><a href="/createcustomer" component={CreateCustomer} on:click>Create</a></li>
</ul>

<Router>
  <Route path="/home" component={Home} />
  <Route path="/customers" component={Customers} />
  <Route path="/createcustomer" component={CreateCustomer} />
</Router>


<style>
	ul#menu li{
		display : inline;
	}
</style>