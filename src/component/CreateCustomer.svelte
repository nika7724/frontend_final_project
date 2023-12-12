
<script>
  import { onMount } from "svelte";
  let customerDetail = {firstName:"", lastName:"", address:"", email:"", statusName:""};
  let statuses = [];
  

  async function fetchStatuses() {
    const response = await fetch("http://localhost:8080/statuses");
    const data = await response.json();
    statuses = data;
  }
  onMount(fetchStatuses);

  async function createCustomer() {
    const createCustomerApi = `http://localhost:8080/customer?statusId=${customerDetail.statusId}`;
    try {
      const endpointCreate = await fetch(createCustomerApi, {
      method: "POST",
      body: JSON.stringify({
        firstName: customerDetail.firstName,
        lastName: customerDetail.lastName,
        address: customerDetail.address,
        email: customerDetail.email,
      }),
      headers: {
        "Content-Type": "application/json; charset=UTF-8"
      }
    });
    const data = await endpointCreate.json();
      console.log(data);
    } catch (error) {
      console.error("Error:", error);
    }
  }

</script>

<div class="container">
  <div class="customer-header">VIP Customer</div>
  <div class="customer-body">
    <form action="" method="post" class="create_customer" id="create_customer">
      <label for="firstName">FirstName</label>
      <input
        id="firstName"
        bind:value={customerDetail.firstName}
        type="text"
        placeholder="FirstName"
        required
        autocomplete="given-name"
      />
      <label for="lastName">LastName</label>
      <input
        id="lastName"
        bind:value={customerDetail.lastName}
        type="text"
        placeholder="LastName"
        required
        autocomplete="family-name"
      />
      <label for="address">Address</label>
      <input
        id="address"
        bind:value={customerDetail.address}
        type="text"
        placeholder="Address"
        required
        autocomplete="address-level1"
      />
      <label for="email">Email</label>
      <input
        id="email"
        bind:value={customerDetail.email}
        type="text"
        placeholder="Email"
        required
        autocomplete="email"
      />
      <label for="statusName">Status</label>
      <select id="statusName" bind:value={customerDetail.statusId}>
        <option value="">--choose status--</option>
        {#each statuses as statusData (statusData.id)}
          <option value={statusData.id}>{statusData.statusName}</option>
        {/each}
      </select>
      <button type="button" on:click={createCustomer}>Add</button>
    </form>
  </div>
</div> 
