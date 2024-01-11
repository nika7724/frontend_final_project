<script>
  import { createEventDispatcher } from "svelte";
  export let customerDetails;
  export let isFirstRow;
  const dispatch = createEventDispatcher();
  let isEditing = false;
  let editedDetails = { ...customerDetails };

  async function deleteCustomer(id) {
    try {
      const response = await fetch(`http://localhost:8080/api/customer/` + id, {
        method: "DELETE",
        headers: {
          "Content-type": "application/json; charset=UTF-8",
        },
      });
      if (response.ok) {
        document.location.reload();
      }
      return response;
    } catch (error) {
      console.error("Error:", error);
    }
  }

  async function editCustomer(id) {
    const editCustomerApi = `http://localhost:8080/api/customer/` + id;
    try {
      const request = await fetch(editCustomerApi, {
        method: "PUT",
        body: JSON.stringify(editedDetails),
        headers: {
          "Content-Type": "application/json; charset=UTF-8",
        },
      });
      if (request.ok) {
        const response = await request.json();
        console.log(response);
        isEditing = false;
        customerDetails = { ...editedDetails };
      } else {
        console.error("Error:", request.statusText);
      }
    } catch (error) {
      console.error("Error:", error);
    }
  }

  function editable() {
    isEditing = true;
    dispatch("editMode", { id: customerDetails.id });
  }

  function cancel() {
    isEditing = false;
    editedDetails = { ...customerDetails };
  }
</script>

{#if isFirstRow}
<div class ="title">
  CUSTOMER LIST
</div>
{/if}


<div class ="container">
<table>
  {#if isFirstRow}
    <thead>
      <tr>
        {#each Object.keys(customerDetails) as key}
          <th>{key.toUpperCase()}</th>
        {/each}
        <th>ACTION</th>
      </tr>
    </thead>
  {/if}

  <tbody>
    <tr>
      {#each Object.entries(customerDetails) as [key, value]}
        {#if key === "status"}
          <td>{value.statusName}</td>
        {:else}
          <td
            contenteditable={isEditing}
            on:input={(event) =>
              (editedDetails[key] = event.target.textContent)}
          >
            {isEditing ? editedDetails[key] : value}
          </td>
        {/if}
      {/each}
      <td>
        {#if isEditing}
          <button
            type="button"
            on:click={() => editCustomer(customerDetails.id)}>Save</button
          >
          <button type="button" on:click={() => cancel()}>Cancel</button>
        {:else}
          <button type="button" on:click={() => editable()}>Edit</button>
        {/if}
        <button
          type="button"
          on:click={() => deleteCustomer(customerDetails.id)}>Delete</button
        >
      </td>
    </tr>
  </tbody>
</table>
</div>

<style>
  .container {
    display: flex;
    justify-content: flex-end;
  }

  table {
    border-collapse: collapse;
  }
  th,
  td {
    border: 1px solid;
    width: 150px;
    height: 50px;
    border-color: #0d5f41;
  }

  .title {
    margin-top: 15px;
    margin-bottom: 20px;
    text-align: center;
  font-size: 35px; 
  color:#0d5f41;
  }

  button {
    background-color: #0d5f41;
    border: white solid 1px;
    height: 23px;
    width: 70px;
    color: white;
    font-size:15px;
    text-align: center;
  }
</style>
