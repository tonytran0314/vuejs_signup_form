<script setup>
    import { ref, defineProps, computed } from 'vue'

    let fullnameError = ref('')
    let checkFill = ref('rgb(98, 116, 139)')

    const props = defineProps({
        label: {
            type: String,
            required: true
        },
        model: {
            type: String,
            required: true
        },
        placeholder: {
            type: String,
            required: true
        },
        type: {
            type: String,
            required: true
        }
    })

</script>

<template>
    <div class="field">
        <label :for="props.model">{{ props.label }}</label>
        <div class="input_field">
            <input 
                v-model.trim="props.model"
                @blur="fullnameValidation"
                :type="props.type" 
                :name="props.model"
                :placeholder="props.placeholder">
            <div class="input_icon">
                <svg 
                    xmlns="http://www.w3.org/2000/svg" 
                    x="0px" y="0px" 
                    width="24" height="24" 
                    viewBox="0 0 48 48">
                        <path 
                            :fill="checkFill" 
                            d="M44,24c0,11.045-8.955,20-20,20S4,35.045,4,24S12.955,4,24,4S44,12.955,44,24z">
                        </path>
                        <path 
                            fill="rgb(255, 255, 255)" 
                            d="M34.586,14.586l-13.57,13.586l-5.602-5.586l-2.828,2.828l8.434,8.414l16.395-16.414L34.586,14.586z">
                        </path>
                </svg>
            </div>
        </div>
        <span v-show="fullnameError" class="field_error">{{ fullnameError }}</span>
    </div>
</template>


<style scoped>
/* SHARE THE CSS WITH PASSWORD AND CONFIRM PASSWORD COMPONENT */
    .field {
        display: flex;
        flex-direction: column;
        gap: 4px;
    }

    .field label {
        color: rgb(98, 116, 139);
        /* background-color: yellow; */
    }

    .field input {
        border: none;
        color: rgb(255, 255, 255);
        padding: 4px 0;
        width: 100%;
        background-color: rgb(14, 23, 39);
        /* background-color: rgb(255, 255, 255); */
    }

    .field input:focus {
        outline: none;
    }

    .input_field {
        border-bottom: 2px solid rgb(16, 32, 53);
        display: flex;
        justify-content: space-between;
        gap: 8px;
        /* background-color: red; */
    }

    .input_icon {
        height: 24px;
        display: flex;
        gap: 16px;
        /* background-color: skyblue; */
    }

    .field_error {
        color: rgb(243, 72, 125);
    }

    .field_error ul {
        margin-left: 32px;
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