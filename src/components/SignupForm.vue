<script setup>
    import FieldBase from './form_components/FieldBase.vue'
    import Password from './form_components/password_component/Password.vue'
    import ConfirmPassword from './form_components/password_component/ConfirmPassword.vue'

    import { ref } from 'vue'
    import { useToast } from "vue-toastification";

    const toast = useToast()

    let hasFieldErrors = ref(true)

    const submitHandle = () => {
        console.log(hasFieldErrors.value)
        if(hasFieldErrors.value === true) {
            toast.error(`You haven't completed the form`)
        } else {
            toast.success('Sign Up Successfully')
        }
    }

    // Nên gôm các biến liên quan đến fullname trong validation vào 1 object
    const fullnameValidation = () => {
        fullnameError.value = ''
        hasFieldErrors.value = false
        const fullnameRegex = /^[a-zA-Z\s]*$/
        const errors = {
            'empty': 'Full name could not be empty',
            'invalid': 'Full name contains invalid characters'
        }
        // check if full name is empty
        if(fullname.value == null || fullname.value == '') { 
            fullnameError.value = errors['empty'] 
        }

        // check if full name contains invalid characters
        if(!fullnameRegex.test(fullname.value)) { 
            fullnameError.value = errors['invalid'] 
        }

        // check if fullnameError is empty => mark the tick blue
        // no error:
        if(fullnameError.value == '' || fullnameError.value == null) {
            fullnameCheckFill.value = 'rgb(50, 138, 241)' // blue
        } else {
            fullnameCheckFill.value = 'rgb(98, 116, 139)'
            hasFieldErrors.value = true
        }
    }

    const emailValidation = () => {
        emailError.value = ''
        hasFieldErrors.value = false
        const emailRegex = /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/
        const errors = {
            'empty': 'Email could not be empty',
            'invalid': 'Invalid or existed email'
        }
        
        if(email.value == null || email.value == '') { 
            emailError.value = errors['empty'] 
        }

        if(!emailRegex.test(email.value)) { 
            emailError.value = errors['invalid'] 
        }

        if(emailError.value == '' || emailError.value == null) {
            emailCheckFill.value = 'rgb(50, 138, 241)'
        } else {
            emailCheckFill.value = 'rgb(98, 116, 139)'
            hasFieldErrors.value = true
        }
    }

    const passwordValidation = () => {
        passwordError.value = ''
        hasFieldErrors.value = false
        const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%])[^\s]{8,}$/

        if(!passwordRegex.test(password.value)) { 
            passwordError.value = true 
        }

        if(passwordError.value == '' || passwordError.value == null) {
            passwordCheckFill.value = 'rgb(50, 138, 241)'
        } else {
            passwordCheckFill.value = 'rgb(98, 116, 139)'
            hasFieldErrors.value = true
        }
    }

    const confirmPasswordValidation = () => {
        confirmPasswordError.value = ''
        hasFieldErrors.value = false
        const errors = {
            'empty': 'Please enter your password again',
            'unmatch': 'Your passwords are not match'
        }

        if(confirmPassword.value == null || confirmPassword.value == '') { 
            confirmPasswordError.value = errors['empty'] 
        }

        if(password.value !== confirmPassword.value ) { 
            confirmPasswordError.value = errors['unmatch'] 
        }

        if(confirmPasswordError.value == '' || confirmPasswordError.value == null) {
            confirmPasswordCheckFill.value = 'rgb(50, 138, 241)'
        } else {
            confirmPasswordCheckFill.value = 'rgb(98, 116, 139)'
            hasFieldErrors.value = true
        }
    }


</script>

<template>
    <form id="signup_form">
        <div class="form_title"><h1>Sign Up</h1></div>
        <div class="form_body">
            <FieldBase 
                label="Full Name"
                model="fullname"
                placeholder="Enter Full Name"
                type="text" />
            <FieldBase 
                label="Email"
                model="email"
                placeholder="Enter Email"
                type="text" />
            <Password 
                label="Password"
                model="password"
                placeholder="Enter Password" />
            <ConfirmPassword 
                label="Confirm Password"
                model="confirmPassword"
                placeholder="Confirm Password" />
        </div>
        <button 
            type="submit"
            id="signup_button" 
            @click.prevent="submitHandle">
                Signup
        </button>
    </form>
</template>

<style scoped>
    #signup_form {
        display: flex;
        flex-direction: column;
        gap: 40px;
        width: 400px;
    }

    .form_title {
        text-align: center;
        color: rgb(255, 255, 255);
    }

    .form_body {
        display: flex;
        flex-wrap: wrap;
        flex-direction: column;
        gap: 24px;
    }

    #signup_button {
        background-color: rgb(50, 138, 241);
        border: none;
        color: rgb(255, 255, 255);
        font-size: 1.1em;
        border-radius: 24px;
        padding: 10px 0;
        cursor: pointer;
    }

    @media (max-width: 524px) {
        #signup_form {
            width: 100%;
        }
    }
</style>