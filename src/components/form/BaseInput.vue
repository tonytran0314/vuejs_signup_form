<script setup>
    import { ref, reactive } from 'vue'
    import EyeSymbol from './icon/EyeSymbol.vue';
    import EyeSlashSymbol from './icon/EyeSlashSymbol.vue';

    const props = defineProps({
        label: {
            type: String,
            required: true
        },
        modelValue: {
            type: String,
            default: ""
        },
        placeholder: {
            type: String,
            required: true
        },
        type: {
            type: String,
            required: true
        },
        name: {
            type: String,
            required: true
        },
        togglePassword: {
            type: Boolean
        },
        error: {
            type: String
        }
    })
    
    const emit = defineEmits(['update:modelValue', 'updateType']) // [Emit] part 1 (these two parts must be together)

    let showPassword = ref(false)
    const togglePassword = () => {
        showPassword.value = !showPassword.value

        let emitType = showPassword.value ? 'text' : 'password'
        emit('updateType', {
            'type': emitType,
            'name': props.name
        })
    }

    const updateModelValue = (event) => {
        const inputValue = event.target.value.trim()
        emit('update:modelValue', inputValue) // [Emit] part 2 (these two parts must be together)
    }

</script>

<template>
    <div class="field">
        <label :for="props.name">{{ props.label }}</label>
        <div class="input_field">
            <input 
                @input="updateModelValue"
                :value="props.modelValue"
                :type="props.type" 
                :name="props.name"
                :placeholder="props.placeholder">
            <div class="input_icon">
                <div v-show="props.togglePassword">
                    <EyeSymbol v-if="showPassword" @toggle-password-visibility="togglePassword" /> 
                    <EyeSlashSymbol v-else @toggle-password-visibility="togglePassword" />
                </div>
            </div>
        </div>
        <span class="field_error">{{ props.error }}</span>
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