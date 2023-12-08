<script>
  import Customers from "./component/Customers.svelte";
  import CreateCustomer from "./component/CreateCustomer.svelte";
  import {Router, Route} from "svelte-routing";

  </script>


<Router>
  <Route path="/customers" component={Customers} />
  <Route path="/createcustomer" component={CreateCustomer} />
</Router>