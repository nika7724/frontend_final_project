<script>
    // import axios from "axios";
    let userDetails ={username: "", password: ""};
    
    function registerSubmit() {
        // axios.post('http://localhost:8080/auth/login', {
        //                 username: userDetails.username,
        //         password: userDetails.password
        
        // })
    fetch('http://localhost:8080/auth/login', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json; charset=UTF-8'
            },
            body: JSON.stringify({
                username: userDetails.username,
                password: userDetails.password,
            })
        })
        .then(response => {
            if (response.ok) {
                window.location.href = '/home';
            } else {
                console.error("Error logging user:", response.statusText);
            }
        })
        .catch(error => {
            console.error("Error logging:", error);
        });
    }
    </script>
    
    <main class="container">
        <form on:submit|preventDefault={registerSubmit}>
            <h2 class="register">Please login</h2>
    
            <div class="form-floating">
                <label for="username">Userame</label>
                <input bind:value={userDetails.username} id="username" type="text" placeholder="Username" required autocomplete="username">
            </div>
            
            <div class="form-floating">
                <label for="password">Password</label>
                <input bind:value={userDetails.password} id="password" type="password"  placeholder="Password" required autocomplete="off">
            </div>
    
            <button class="w-100 btn btn-lg btn-primary" type="submit">Submit</button>
        </form>
    </main>
    
    <style>
    
        .register {
            margin-left: 10px;
            color: #0d5f41;
        }
        
        .container {
        background-color: #f7ddc6;
        width: 400px;
        height: 400px;
        margin-left: 500px;
      }
    
    label {
        font-size:var(--text-font-size) ;
        color: #0d5f41;
        display: inline-block;
        width: 300px;
        height: 30px;
        margin-top: 30px;
        margin-left: 50px;
    }
    
    input {
        width: 300px;
        height: 30px;
        border: none;
        background-color: white;
        color:#0d5f41;
        margin-left: 50px;
    }
    
    button {
        width: 80px;
        height: 40px;
        text-align: center;
        margin-left: 10px;
        position:absolute;
        top:320px;
        left:660px;
        background: #0d5f41;
        color:white;
        border: none;
    }
    
    button:hover {
        color:lightgray;
    }
        
        </style>