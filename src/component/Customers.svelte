<script>
    import { onMount } from "svelte";
    import CustomerList from "./CustomerList.svelte";
    import CreateCustomer from "./CreateCustomer.svelte";
    let customers = [];
    let role =[];

//     async function fetchRoles() {
//     const response = await fetch("http://localhost:8080/roles");
//     const data = await response.json();
//     role = data;
//   }
//   onMount(fetchRoles);

  
    const customerList = "http://localhost:8080/customers";

    onMount(async () => {
        const response = await fetch(customerList);
        const res = await response.json();
        console.log(res);
        customers = res;
        if (response.status == 200) {
            console.log(response.status);
        } else {
            console.log("An error occured");
            console.log(request.status);
        }
    });
</script>

<section>
    {#each customers as customerInfo, i}
        <!-- {#each customers as customerInfo}
    <CustomerList customerDetails={customerInfo} /> -->
        <CustomerList customerDetails={customerInfo} isFirstRow={i === 0} />
    {/each}
</section>

<div>
    <a href="/createcustomer">
      <button class="create_btn" component={CreateCustomer} on:click>Create</button>
    </a>
  </div>

  <style>
button {
    margin-left: 250px;
}

    </style>