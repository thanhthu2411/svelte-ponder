<script>
    let email = $state("")
    let password = $state("")

    const loginHandler = (e) => {
        
        e.preventDefault()
        console.log("Button clicked")

        if (password.length < 6) {
            console.log("Password is too short")
        }
    
    }
</script>

<form onsubmit={(e) => loginHandler(e)}>
    <div class="form-group">
        <label>Email</label>
        <input bind:value={email} id="email" required name="email" placeholder="Email" type="email" />
    </div>
    <div class="form-group"> 
        <label>Password</label>
        <input bind:value={password} required id="password" name="password" placeholder="Password" type="password" />
    </div>
    <button type="submit">Log In</button>
</form>

<style>
    form {
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        gap: 20px;

        margin-top: 2rem;
        border: 1px solid lightgray;
        border-radius: 10px;
        padding: 25px;
        
    }
    .form-group {
        display: flex;
        flex-direction: row;
        gap: 20px;
        justify-content: space-between;
    }

    input {
        padding: 5px 10px;
        border-radius: 5px;
    }
</style>