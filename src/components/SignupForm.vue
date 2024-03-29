<script setup>
    const submitHandle = () => {
        alert('Clicked')
    }
</script>

<template>
    <form id="signup_form">
        <div class="form_title"><h1>Sign Up</h1></div>
        <div class="field">
            <label for="fullname">Full Name</label>
            <input 
                type="text" 
                id="fullname" 
                name="fullname"
                placeholder="Enter Full Name">
        </div>
        <div class="field">
            <label for="email">Email</label>
            <input 
                type="text" 
                id="email" 
                name="email"
                placeholder="Enter Email">
        </div>
        <div class="field">
            <label for="password">Password</label>
            <input 
                type="password" 
                id="password" 
                name="fullname"
                placeholder="Enter Password">
        </div>
        <div class="field">
            <label for="confirm_password">Confirm Password</label>
            <input 
                type="password" 
                id="confirm_password" 
                name="confirm_password"
                placeholder="Enter Password Again">
        </div>
        <button type="submit" @click.prevent="submitHandle">Signup</button>
    </form>
</template>

<style scoped>
    #signup_form {
        display: flex;
        flex-direction: column;
        gap: 24px;
        width: 400px;
    }
    .form_title {
        text-align: center;
        color: rgb(255, 255, 255);
    }
    .field {
        display: flex;
        flex-direction: column;
        gap: 4px;
        border-bottom: 2px solid rgb(16, 32, 53);
    }

    .field label {
        color: rgb(98, 116, 139);
    }

    .field input {
        background-color: rgb(14, 23, 39);
        /* background-color: rgb(255, 255, 255); */
        border: none;
        color: rgb(255, 255, 255);
        padding: 4px 0;
    }
    .field input:focus {
        outline: none;
    }
    button {
        background-color: rgb(50, 138, 241);
        border: none;
        color: rgb(255, 255, 255);
        font-size: 1.1em;
        border-radius: 24px;
        padding: 10px 0;
        cursor: pointer;
    }

    ::placeholder {
        color: rgb(65, 79, 96);
        opacity: 1; /* Firefox */
        font-size: 1.1em;
    }

    ::-ms-input-placeholder { /* Edge 12-18 */
        color: rgb(65, 79, 96);
        font-size: 1.1em;
    }
</style>