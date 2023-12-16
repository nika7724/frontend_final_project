<script>
  import Customers from "./component/Customers.svelte";
  import CreateCustomer from "./component/CreateCustomer.svelte";
  import Home from "./component/Home.svelte";
  import { Router, Route } from "svelte-routing";
</script>

  <div class="sidebar">
    <div class="title">
      Menu
  </div>
<ul class="links">
	<li><a href="/home" component={Home} on:click>Home</a></li> 
	<li><a href="/createcustomer" component={CreateCustomer} on:click>Create</a></li>
	<li><a href="/customers" component={Customers} on:click>Customer</a></li> 
</ul>
</div>


<Router>
  <Route path="/home" component={Home} />
  <Route path="/customers" component={Customers} />
  <Route path="/createcustomer" component={CreateCustomer} />
</Router>


<style>

.sidebar {
    width: 170px;
    position: absolute;
    height: 100%;
    background: #0d5f41;
    transition: 0.5s;
}

.sidebar .title {
    padding-left: 50px;
    font-size: 25px;
    line-height: 60px;
    color: white;
    border-bottom: 2px solid lightgray;
}

.sidebar .links {
    padding: 0 !important;
    margin-top: 0 !important; 
}

.sidebar  .links li{
    list-style: none;
    display: block;
    line-height: 60px;
    border-bottom: 2px solid lightgray;
    cursor: pointer;
    margin: 0;
    width: 100%;
}

.sidebar .links li:hover{
  background: #333;
  border-left: 1px solid white;
}

.sidebar .links li a{
  text-decoration: none;
  color: white;
  font-size: 20px;
  padding-left: 10px;
  transition: 0.5s;
  box-sizing: border-box;
}

.sidebar .links li:hover a{
  color: lightgray;
  letter-spacing: 1.2px;
}

</style>  