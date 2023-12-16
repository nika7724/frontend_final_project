
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

<div class="customer-header">CREATE CUSTOMER</div>

<div class="container">
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
      <button type="button" on:click={createCustomer}>Save</button>
    </form>
  </div>

<style>

.container {
    background-color: #f7ddc6;
    width: 600px;
    height: 550px;
    margin-left: 400px;
  }

  label {
    font-size:var(--text-font-size) ;
    color: #0d5f41;
    display: inline-block;
    width: 300px;
    height: 30px;
    margin-top: 30px;
    margin-left: 150px;
}

.customer-header {
   padding-left: 520px;
    margin-bottom: 22px;
  font-size: 35px; 
  color:#0d5f41;
}


input, select{
    width: 300px;
    height: 30px;
    border: none;
    background-color: white;
    color:#0d5f41;
    margin-left: 150px;
}

button {
    width: 80px;
    height: 40px;
    text-align: center;
    margin-left: 10px;
    position:absolute;
    top:555px;
    left:650px;
    background: #0d5f41;
    color:white;
    border: none;
}

button:hover {
    color:lightgray;
}

  </style>