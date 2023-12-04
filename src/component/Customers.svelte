<script>
    import { onMount } from "svelte";
    import CustomerList from "./CustomerList.svelte";
    let customers = [];

    const customerList = "http://localhost:8080/customers";

    onMount(async () => {
        const response = await fetch(customerList);
        const res = await response.json();
        console.log(res);
        customers = res;
    });
</script>

<section>
    {#each customers as customerInfo, i}
        <CustomerList customerDetails={customerInfo} isFirstRow={i === 0} />
    {/each}
</section>
