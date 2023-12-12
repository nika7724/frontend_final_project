<!-- <script>
   export {deleteCustomer};

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
</script> -->