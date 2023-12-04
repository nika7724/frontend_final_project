<script>
    import { onMount } from "svelte";
    import CustomerList from "./CustomerList.svelte";
    let customers = [];
    let temp = [];

    const customerList = "http://localhost:8080/customers";

    onMount(async () => {
        const response = await fetch(customerList);
        const res = await response.json();
        console.log(res);
        customers = res;
    });

    for (let i = 0; i < customers.length; i++) {
      customers[i].status.forEach((status) => {
          temp.push({
            statusName: status.statusName,
          });
        });
        }
</script>

<section>
    {#each customers as customerInfo}
        <CustomerList customerDetails ={customerInfo} />
    {/each}
</section>

