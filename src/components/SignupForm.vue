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

    const completedFieldColor = ref('rgb(50, 138, 241)')
    const notcompletedFieldColor = ref('rgb(98, 116, 139)')
    
    const fullname = ref('')
    const email = ref('')
    const password = ref('')
    const confirmPassword = ref('')

    // Nên gôm các biến liên quan đến fullname trong validation vào 1 object
    const fullnameValidation = (fullname) => {
        let error = {
            'exist': false,
            'message': null
        }

        const errors_list = {
            'empty': 'Full name could not be empty',
            'invalid': 'Full name contains invalid characters'
        }

        const fullnameRegex = /^[a-zA-Z\s]*$/

        // check if full name is empty
        if(fullname == null || fullname == '') { 
            error = {
                'exist': true,
                'message': errors_list.empty
            }
        }

        // check if full name contains invalid characters (valid: a-z, A-Z and space)
        if(!fullnameRegex.test(fullname)) { 
            error = {
                'exist': true,
                'message': errors_list.invalid
            }
        }

        return error;
    }

    const emailValidation = (email) => {
        let error = {
            'exist': false,
            'message': null
        }

        const errors_list = {
            'invalid': 'Invalid email'
        }

        const emailRegex = /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/

        if(!emailRegex.test(email)) { 
            error = {
                'exist': true,
                'message': errors_list.invalid
            }
        }

        return error;
    }

    const passwordValidation = (password) => {
        let error = {
            'exist': false,
            'message': null
        }

        const errors_list = {
            'invalid': 'Invalid password'
        }

        const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%])[^\s]{8,}$/

        if(!passwordRegex.test(password)) { 
            error = {
                'exist': true,
                'message': errors_list.invalid
            }
        }
        return error;
    }

    const confirmPasswordValidation = (confirmPassword) => {
        let error = {
            'exist': false,
            'message': null
        }

        const errors_list = {
            'unmatch': 'Your passwords are not match'
        }

        if(password.value !== confirmPassword ) { 
            error = {
                'exist': true,
                'message': errors_list.unmatch
            }
        }
        return error
    }

</script>

<template>
    <form id="signup_form">
        <div class="form_title"><h1>Sign Up</h1></div>
        <div class="form_body">
            <FieldBase 
                label="Full Name"
                v-model="fullname"
                placeholder="Enter Full Name"
                type="text" 
                name="fullname"
                :validator="fullnameValidation" />
            <FieldBase 
                label="Email"
                v-model="email"
                placeholder="Enter Email"
                type="text"
                name="email"
                :validator="emailValidation" />
            <Password 
                label="Password"
                v-model="password"
                name="password"
                placeholder="Enter Password"
                :validator="passwordValidation" />
            <ConfirmPassword 
                label="Confirm Password"
                v-model="confirmPassword"
                name="confirmPassword"
                placeholder="Confirm Password"
                :validator="confirmPasswordValidation" />
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