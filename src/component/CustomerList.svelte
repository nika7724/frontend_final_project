<script>
    export let customerDetails;
    export let isFirstRow;
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
                    <button class = "edit_btn">Edit</button>
                    <button class = "delete_btn">Delete</button>
                    <button class = "create_btn">Create</button>
                  </td>
            </tr>
        </tbody>
    </table>
   
    <style>
      th,
      td {
        border: 1px solid;
        width: 135px;
          }
    
      </style>