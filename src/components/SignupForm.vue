<script setup>
    import { ref, reactive } from 'vue'
    import { useToast } from "vue-toastification";
    import BaseInput from './form/BaseInput.vue'

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
            'empty': 'Password could not be empty',
            'invalid': 'Password contains invalid characters'
        }

        // const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[!@#$%])[^\s]{8,}$/
        const passwordRegex = /^[a-zA-Z0-9\!@#$%]*$/

        if(password == null || password == '') { 
            error = {
                'exist': true,
                'message': errors_list.empty
            }
        }

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
            'empty': 'Password could not be empty',
            'unmatch': 'Your passwords are not match'
        }

        if(confirmPassword == null || confirmPassword == '') { 
            error = {
                'exist': true,
                'message': errors_list.empty
            }
        }

        if(password.value !== confirmPassword ) { 
            error = {
                'exist': true,
                'message': errors_list.unmatch
            }
        }
        return error
    }

    const updateInputType = (field) => {
        if (field.name === 'password') {
            password.type = field.type
        }

        if (field.name === 'confirmPassword') {
            confirmPassword.type = field.type
        }
    }

    const fullname = reactive({
        'vmodel': '',
        'type': 'text',
        'name': 'fullname',
        'label': 'Full Name',
        'placeholder': 'Enter Full Name',
        'validator': fullnameValidation
    })

    const email = reactive({
        'vmodel': '',
        'type': 'text',
        'name': 'email',
        'label': 'Email',
        'placeholder': 'Enter Email',
        'validator': emailValidation
    })

    const password = reactive({
        'vmodel': '',
        'type': 'password',
        'name': 'password',
        'label': 'Password',
        'placeholder': 'Enter Password',
        'validator': passwordValidation,
        'toggle': true
    })

    const confirmPassword = reactive({
        'vmodel': '',
        'type': 'password',
        'name': 'confirmPassword',
        'label': 'Confirm Password',
        'placeholder': 'Enter Password Again',
        'validator': confirmPasswordValidation,
        'toggle': true
    })
</script>

<template>
    <form id="signup_form">
        <div class="form_title"><h1>Sign Up</h1></div>
        <div class="form_body">
            <BaseInput
                v-model="fullname.vmodel"
                :type="fullname.type"
                :name="fullname.name"
                :label="fullname.label"
                :placeholder="fullname.placeholder"
                :validator="fullname.validator" />

            <BaseInput
                v-model="email.vmodel"
                :type="email.type"
                :name="email.name"
                :label="email.label"
                :placeholder="email.placeholder"
                :validator="email.validator" />

            <BaseInput
                v-model="password.vmodel"
                :type="password.type"
                :name="password.name"
                :label="password.label"
                :placeholder="password.placeholder"
                :validator="password.validator"
                :togglePassword="password.toggle"
                @updateType="updateInputType" />

            <BaseInput
                v-model="confirmPassword.vmodel"
                :type="confirmPassword.type"
                :name="confirmPassword.name"
                :label="confirmPassword.label"
                :placeholder="confirmPassword.placeholder"
                :validator="confirmPassword.validator"
                :togglePassword="confirmPassword.toggle"
                @updateType="updateInputType" />

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