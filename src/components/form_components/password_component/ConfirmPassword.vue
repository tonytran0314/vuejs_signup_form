<script setup>
    import { ref, reactive, computed } from 'vue'
    import EyeSymbol from './EyeSymbol.vue'
    import EyeSlashSymbol from './EyeSlashSymbol.vue'

    const props = defineProps({
        label: {
            type: String,
            required: true
        },
        modelValue: {
            type: String,
            required: true
        },
        placeholder: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        validator: {
            type: Function,
            required: true
        }
    })

    let showPassword = ref(false)
    const togglePassword = () => showPassword.value = !showPassword.value
    const inputType = computed(() =>  showPassword.value ? 'text' : 'password')

    const error = reactive({
        'exist': true,
        'message': null
    })

    const emit = defineEmits(['update:modelValue']) // [Emit] part 1 (these two parts must be together)

    const blueColor = ref('rgb(50, 138, 241)') // completed color
    const grayColor = ref('rgb(98, 116, 139)')

    const updateModelValueAndValidate = (event) => {
        const inputValue = event.target.value.trim()

        error.exist = props.validator(inputValue).exist
        error.message = props.validator(inputValue).message

        emit('update:modelValue', inputValue) // [Emit] part 2 (these two parts must be together)
    }
</script>

<template>
    <div class="field">
        <label :for="props.model">{{ props.label }}</label>
        <div class="input_field">
            <input 
                :value="props.modelValue"
                @input="updateModelValueAndValidate"
                @blur="updateModelValueAndValidate"
                :type="inputType" 
                :name="props.name"
                :placeholder="props.placeholder">
            <div class="input_icon">
                
                <EyeSymbol v-if="showPassword" @toggle-password-visibility="togglePassword" /> 
                <EyeSlashSymbol v-else @toggle-password-visibility="togglePassword" />

                <svg 
                    xmlns="http://www.w3.org/2000/svg" 
                    x="0px" y="0px" 
                    width="24" height="24" 
                    viewBox="0 0 48 48">
                        <path 
                            :fill="error.exist ? grayColor : blueColor"
                            d="M44,24c0,11.045-8.955,20-20,20S4,35.045,4,24S12.955,4,24,4S44,12.955,44,24z">
                        </path>
                        <path 
                            fill="rgb(255, 255, 255)" 
                            d="M34.586,14.586l-13.57,13.586l-5.602-5.586l-2.828,2.828l8.434,8.414l16.395-16.414L34.586,14.586z">
                        </path>
                </svg>
            </div>
        </div>
        <span class="field_error">{{ error.message }}</span>
    </div>
</template>

<style scoped>
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