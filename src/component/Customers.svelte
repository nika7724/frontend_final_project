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

<div><button class="create_btn">Create</button></div>
