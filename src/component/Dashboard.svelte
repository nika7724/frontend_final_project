<!-- <script>
    import {onMount} from 'svelte';
    import axios from "axios";
    import { navigate } from 'svelte-routing';
 
    let message = 'You are not logged in';
 
    onMount(async () => {
        const response = await axios.get('http://localhost:8080/user/');
 
        if (response.status === 200) {
            message = `Hi ${response.data.username}`;
        } else {
            navigate ('/login');
        }
    });
 
    $: logout = async () => {
        await axios.post('logout', {}, {withCredentials: true});
 
        axios.defaults.headers.common['Authorization'] = '';
 
        navigate('/login');
    }
 </script>
 
 
 <div class="container mt-5 text-center">
    <h3>{message}</h3>
 
    <a href="/login" class="btn btn-lg btn-primary"
       on:click={logout}
    >Logout</a>
 </div> -->
