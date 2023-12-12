<script>
    export let customerDetails;
    export let isFirstRow;

  
  async function deleteCustomer(id) {
    try {
  const response = await fetch(`http://localhost:8080/customer/` + id, {
  method: 'DELETE', 
  headers: {
  'Content-type': 'application/json; charset=UTF-8',  
 },
})
 if (response.ok) {
        document.location.reload();
    }
    return response;
  } catch (error) {
      console.error('Error:', error);
    }
}

async function editCustomer(id) {
  const editCustomerApi = `http://localhost:8080/customer/` + id;
  try{
  const request = await fetch (editCustomerApi, {
  method: 'PUT', 
  body:  JSON.stringify(customerDetails),
  headers: {
        "Content-Type": "application/json; charset=UTF-8"
      }
  });
  if (request.ok) {
      const response = await request.json();
      console.log(response);
    } else {
      console.error('Error:', request.statusText);
    }
  } catch (error) {
    console.error('Error:', error);
  }
}
    
</script>

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
                  {#if key === 'status'}
                  <td>{value.statusName}</td>
                  {:else}
                  <td>{value}</td>
                  {/if}
                {/each}
                <td>
                  <button type="button" on:click={() =>editCustomer(customerDetails.id)}>Edit</button>
                  <button type="button" on:click={() =>deleteCustomer(customerDetails.id)}>Delete</button></td>
            </tr>
        </tbody>
    </table>
   
    <style>
      th,
      td {
        border: 1px solid;
        width: 150px;
        height: 50px;
          }
    
      </style>