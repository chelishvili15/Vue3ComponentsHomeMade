<!-- 
    * <CheckBox 
    *    v-model:checked="<Boolean variable name>"
    *    fieldId="<Id for label>" - required
    *    label="<Label name if name exist>" 
    *    disable="<Boolean true if disabled>"
    *    color="<'gray' if checkbox is dark>"
    * />
 -->
<template>
    <div class="flex -space-x-4">
        <input
            :id="fieldId"
            ref="input"
            type="checkbox"
            :checked="checked"
            class="opacity-0"
            :disabled="props.disable"
            @focus="focus = true"
            @focusout="focus = false"
            @input="(event) => $emit('update:checked', event.target.checked)"
        />

        <label v-if="props.color === 'white'" :for="fieldId" class="flex space-x-2">
            <div
                class="checkBox flex items-center justify-center"
                :class="[
                    props.checked ? 'bg-green-50' : 'bg-gray-20',
                    props.disable ? 'bg-gray-30' : '',
                    focus ? 'border-1' : '',
                ]"
            >
                <CheckboxCheck
                    v-show="props.checked"
                    :color="props.disable ? '#c5c5c5' : 'white'"
                />
            </div>
            <p :class="props.disable ? '' : ''">
                {{ label }}
            </p>
        </label>
        <!-- this label for darkMode -->
        <label v-else-if="props.color === 'gray'" :for="fieldId" class="flex space-x-2">
            <div
                class="checkBox flex items-center justify-center bg-gray-90"
                :class="[
                    focus ? 'border-1' : '',
                ]"
            >
                <CheckboxCheck
                    v-show="props.checked"
                    :color="props.disable ? '#878787' : '#5E5E5E'"
                />
            </div>
            <p :class="props.disable ? '' : ''">
                {{ label }}
            </p>
        </label>
    </div>
</template>

<script setup>
import { ref } from "vue";
import CheckboxCheck from "@/assets/icons/CheckboxCheck.vue";

const input = ref(null);
const focus = ref(false);

defineEmits(["update:checked"]);
const props = defineProps({
    label: {
        type: String,
        default: "",
    },
    checked: {
        type: Boolean,
    },
    fieldId: {
        type: String,
        required: true,
    },
    disable: {
        type: Boolean,
    },
    color: {
        type: String,
        default: 'white',
    }
});
</script>

<style scoped>
.checkBox {
    height: 20px;
    width: 20px;
    border-radius: 6px;
}
.border-1 {
    border: 1px solid black;
}
</style>
