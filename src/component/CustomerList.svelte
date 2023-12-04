<script>
    export let customerDetails;
</script>

    <table>
        <thead>
            <tr>
                {#each Object.keys(customerDetails) as key}
                  <th>{key}</th>
                {/each}
              </tr>
        </thead>
        
        <tbody>
            <tr>
                {#each Object.entries(customerDetails) as [key, value]}
                  {#if key === 'status'}
                  <td>{value.statusName}</td>
                  {:else}
                  <td>{value}</td>
                  {/if}
                {/each}
            </tr>
        </tbody>
    </table>
