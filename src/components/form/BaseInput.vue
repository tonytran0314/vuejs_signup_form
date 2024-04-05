<script setup>
    import { ref } from 'vue'
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
            <div v-show="props.togglePassword">
                <EyeSymbol v-if="showPassword" @toggle-password-visibility="togglePassword" /> 
                <EyeSlashSymbol v-else @toggle-password-visibility="togglePassword" />
            </div>
        </div>
        <span class="field_error">{{ props.error }}</span>
    </div>
</template>


<style lang="scss" scoped>
    @import '../../assets/variables';

    .field {
        @include displayColumn($baseDistance / 2);

        label {
            color: $labelColor;
        }
        
        .input_field {
            @include displayRow($baseDistance);
            border-bottom: $baseDistance/4 solid $inputBottomBorderColor;
            justify-content: space-between;

            input {
                @include input();

                &:focus {
                    outline: none;
                }

                &::placeholder {
                    color: $placeHolderColor; 
                    opacity: 1; /* Firefox */
                    font-size: 1.1em;
                }

                &::-ms-input-placeholder { /* Edge 12-18 */
                    color: $placeHolderColor;
                    font-size: 1.1em;
                }
            }
        }

        .field_error {
            color: $errorColor;
        }
    }

</style>