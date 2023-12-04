<script>
    export let customerDetails;
    export let isFirstRow;
</script>

    <table>
        {#if isFirstRow}
        <thead>
            <tr>
                {#each Object.keys(customerDetails) as key}
                  <th>{key}</th>
                {/each}
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
            </tr>
        </tbody>
    </table>