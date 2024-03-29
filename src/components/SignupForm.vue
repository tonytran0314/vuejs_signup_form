<script setup>
    import {ref} from 'vue';

    let showPassword = ref(false);
    let showConfirmPassword = ref(false);

    const submitHandle = () => {
        alert('Clicked')
    }

    const togglePassword = () => {
        showPassword.value = !showPassword.value
    }

    const toggleConfirmPassword = () => {
        showConfirmPassword.value = !showConfirmPassword.value
    }
</script>

<template>
    <form id="signup_form">
        <div class="form_title"><h1>Sign Up</h1></div>
        <div class="form_body">
            <div class="field">
                <label for="fullname">Full Name</label>
                <div class="input_field">
                    <input 
                        type="text" 
                        id="fullname" 
                        name="fullname"
                        placeholder="Enter Full Name">
                    <div class="input_icon">
                        <svg 
                            xmlns="http://www.w3.org/2000/svg" 
                            x="0px" y="0px" 
                            width="24" height="24" 
                            viewBox="0 0 48 48">
                                <path 
                                    fill="rgb(98, 116, 139)" 
                                    d="M44,24c0,11.045-8.955,20-20,20S4,35.045,4,24S12.955,4,24,4S44,12.955,44,24z">
                                </path>
                                <path 
                                    fill="rgb(255, 255, 255)" 
                                    d="M34.586,14.586l-13.57,13.586l-5.602-5.586l-2.828,2.828l8.434,8.414l16.395-16.414L34.586,14.586z">
                                </path>
                        </svg>
                    </div>
                </div>
                <span class="field_error">asdkajs</span>
            </div>
            <div class="field">
                <label for="email">Email</label>
                <div class="input_field">
                    <input 
                        type="text" 
                        id="email" 
                        name="email"
                        placeholder="Enter Email">
                    <div class="input_icon">
                        <svg 
                            xmlns="http://www.w3.org/2000/svg" 
                            x="0px" y="0px" 
                            width="24" height="24" 
                            viewBox="0 0 48 48">
                                <path 
                                    fill="rgb(98, 116, 139)" 
                                    d="M44,24c0,11.045-8.955,20-20,20S4,35.045,4,24S12.955,4,24,4S44,12.955,44,24z">
                                </path>
                                <path 
                                    fill="rgb(255, 255, 255)" 
                                    d="M34.586,14.586l-13.57,13.586l-5.602-5.586l-2.828,2.828l8.434,8.414l16.395-16.414L34.586,14.586z">
                                </path>
                        </svg>
                    </div>
                </div>
                <span class="field_error">asdkajs</span>
            </div>
            <div class="field password_field">
                <label for="password">Password</label>
                <div class="input_field">
                    <input 
                        :type="showPassword ? 'text ' : 'password'" 
                        id="password" 
                        name="fullname"
                        placeholder="Enter Password">
                    <div class="input_icon">
                        <!-- hide password -->
                        <svg 
                            v-if="showPassword == false"
                            @click="togglePassword"
                            class="hide_password"
                            width="24px" height="24px" 
                            viewBox="0 0 24 24" 
                            fill="none" 
                            xmlns="http://www.w3.org/2000/svg">
                                <path 
                                    d="M2 2L22 22" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <path 
                                    d="M6.71277 6.7226C3.66479 8.79527 2 12 2 12C2 12 5.63636 19 12 19C14.0503 19 15.8174 18.2734 17.2711 17.2884M11 5.05822C11.3254 5.02013 11.6588 5 12 5C18.3636 5 22 12 22 12C22 12 21.3082 13.3317 20 14.8335" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <path 
                                    d="M14 14.2362C13.4692 14.7112 12.7684 15.0001 12 15.0001C10.3431 15.0001 9 13.657 9 12.0001C9 11.1764 9.33193 10.4303 9.86932 9.88818" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                        </svg>
                        <!-- show password -->
                        <svg 
                            v-if="showPassword == true"
                            @click="togglePassword"
                            class="show_password"
                            width="24px" height="24px" 
                            viewBox="0 0 24 24" 
                            fill="none" 
                            xmlns="http://www.w3.org/2000/svg">
                                <path 
                                    d="M1 12C1 12 5 4 12 4C19 4 23 12 23 12" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <path 
                                    d="M1 12C1 12 5 20 12 20C19 20 23 12 23 12" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <circle 
                                    cx="12" cy="12" r="3" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                        </svg>
                        <svg 
                            xmlns="http://www.w3.org/2000/svg" 
                            x="0px" y="0px" 
                            width="24" height="24" 
                            viewBox="0 0 48 48">
                                <path 
                                    fill="rgb(98, 116, 139)" 
                                    d="M44,24c0,11.045-8.955,20-20,20S4,35.045,4,24S12.955,4,24,4S44,12.955,44,24z">
                                </path>
                                <path 
                                    fill="rgb(255, 255, 255)" 
                                    d="M34.586,14.586l-13.57,13.586l-5.602-5.586l-2.828,2.828l8.434,8.414l16.395-16.414L34.586,14.586z">
                                </path>
                        </svg>
                    </div>
                </div>
                <span class="field_error">asdkajs</span>
            </div>
            <div class="field password_field">
                <label for="confirm_password">Confirm Password</label>
                <div class="input_field">
                    <input 
                        :type="showConfirmPassword ? 'text ' : 'password'" 
                        id="confirm_password" 
                        name="confirm_password"
                        placeholder="Enter Password Again">
                    <div class="input_icon">
                        <!-- hide password -->
                        <svg 
                            v-if="!showConfirmPassword"
                            @click="toggleConfirmPassword"
                            class="hide_password"
                            width="24px" height="24px" 
                            viewBox="0 0 24 24" 
                            fill="none" 
                            xmlns="http://www.w3.org/2000/svg">
                                <path 
                                    d="M2 2L22 22" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <path 
                                    d="M6.71277 6.7226C3.66479 8.79527 2 12 2 12C2 12 5.63636 19 12 19C14.0503 19 15.8174 18.2734 17.2711 17.2884M11 5.05822C11.3254 5.02013 11.6588 5 12 5C18.3636 5 22 12 22 12C22 12 21.3082 13.3317 20 14.8335" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <path 
                                    d="M14 14.2362C13.4692 14.7112 12.7684 15.0001 12 15.0001C10.3431 15.0001 9 13.657 9 12.0001C9 11.1764 9.33193 10.4303 9.86932 9.88818" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                        </svg>
                        <!-- show password -->
                        <svg 
                            v-if="showConfirmPassword"
                            @click="toggleConfirmPassword"
                            class="show_password"
                            width="24px" height="24px" 
                            viewBox="0 0 24 24" 
                            fill="none" 
                            xmlns="http://www.w3.org/2000/svg">
                                <path 
                                    d="M1 12C1 12 5 4 12 4C19 4 23 12 23 12" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <path 
                                    d="M1 12C1 12 5 20 12 20C19 20 23 12 23 12" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                                <circle 
                                    cx="12" cy="12" r="3" 
                                    stroke="rgb(98, 116, 139)" 
                                    stroke-width="2" 
                                    stroke-linecap="round" 
                                    stroke-linejoin="round"/>
                        </svg>
                        <svg 
                            xmlns="http://www.w3.org/2000/svg" 
                            x="0px" y="0px" 
                            width="24" height="24" 
                            viewBox="0 0 48 48">
                                <path 
                                    fill="rgb(98, 116, 139)" 
                                    d="M44,24c0,11.045-8.955,20-20,20S4,35.045,4,24S12.955,4,24,4S44,12.955,44,24z">
                                </path>
                                <path 
                                    fill="rgb(255, 255, 255)" 
                                    d="M34.586,14.586l-13.57,13.586l-5.602-5.586l-2.828,2.828l8.434,8.414l16.395-16.414L34.586,14.586z">
                                </path>
                        </svg>
                    </div>
                </div>
                <span class="field_error">asdkajs</span>
            </div>
        </div>
        <button 
            type="submit" 
            @click.prevent="submitHandle">Signup</button>
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
        flex-direction: column;
        gap: 24px;
    }

    .field {
        display: flex;
        flex-direction: column;
        gap: 4px;
    }

    .input_field {
        position: relative;
        border-bottom: 2px solid rgb(16, 32, 53);
        /* background-color: red; */
    }

    .input_icon {
        position: absolute;
        right: 0;
        top: 0;
        /* background-color: skyblue; */
        height: 24px;
        display: flex;
        gap: 16px;
    }

    .hide_password, .show_password {
        cursor: pointer;
    }

    .field label {
        color: rgb(98, 116, 139);
        /* background-color: yellow; */
    }

    .field input {
        background-color: rgb(14, 23, 39);
        /* background-color: rgb(255, 255, 255); */
        border: none;
        color: rgb(255, 255, 255);
        padding: 4px 0;
        width: calc(100% - 32px);
    }

    .password_field input {
        width: calc(100% - 72px);
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

    .field_error {
        color: rgb(243, 72, 125);
        display: none;
    }
</style>