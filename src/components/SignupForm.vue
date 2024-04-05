<script setup>
    import { ref, reactive } from 'vue'
    import { useToast } from "vue-toastification";
    import BaseInput from './form/BaseInput.vue'

    const toast = useToast()

    const submitHandle = () => {
        const fullnameError = fullnameValidation(fullname.vmodel)
        const emailError = emailValidation(email.vmodel)
        const passwordError = passwordValidation(password.vmodel)
        const confirmPasswordError = confirmPasswordValidation(confirmPassword.vmodel)

        fullname.error = fullnameError.exist ? fullnameError.message : null
        email.error = emailError.exist ? emailError.message : null
        password.error = passwordError.exist ? passwordError.message : null
        confirmPassword.error = confirmPasswordError.exist ? confirmPasswordError.message : null

        if (!fullname.error && 
            !email.error && 
            !password.error && 
            !confirmPassword.error) {
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
        
        if(password.vmodel !== confirmPassword ) { 
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
        'error': null
    })

    const email = reactive({
        'vmodel': '',
        'type': 'text',
        'name': 'email',
        'label': 'Email',
        'placeholder': 'Enter Email',
        'error': null
    })

    const password = reactive({
        'vmodel': '',
        'type': 'password',
        'name': 'password',
        'label': 'Password',
        'placeholder': 'Enter Password',
        'toggle': true,
        'error': null
    })

    const confirmPassword = reactive({
        'vmodel': '',
        'type': 'password',
        'name': 'confirmPassword',
        'label': 'Confirm Password',
        'placeholder': 'Enter Password Again',
        'toggle': true,
        'error': null
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
                :error="fullname.error" />

            <BaseInput
                v-model="email.vmodel"
                :type="email.type"
                :name="email.name"
                :label="email.label"
                :placeholder="email.placeholder"
                :error="email.error" />

            <BaseInput
                v-model="password.vmodel"
                :type="password.type"
                :name="password.name"
                :label="password.label"
                :placeholder="password.placeholder"
                :togglePassword="password.toggle"
                :error="password.error"
                @updateType="updateInputType" />

            <BaseInput
                v-model="confirmPassword.vmodel"
                :type="confirmPassword.type"
                :name="confirmPassword.name"
                :label="confirmPassword.label"
                :placeholder="confirmPassword.placeholder"
                :togglePassword="confirmPassword.toggle"
                :error="confirmPassword.error"
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

<style lang="scss" scoped>
    @import '../assets/variables';

    #signup_form {
        @include displayColumn($baseDistance * 5);
        width: $baseDistance * 50;

        .form_title {
            text-align: center;
            color: $white;
        }

        .form_body {
            @include displayColumn($baseDistance * 3);
        }

        #signup_button {
            @include button($buttonBackgroundColor);
        }
    }

    @media (max-width: $baseDistance * 66) {
        #signup_form {
            width: 100%;
        }
    }
</style>