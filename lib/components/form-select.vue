<template>
    <select :class="['form-control',inputClass,custom?'custom-select':null]"
            :name="name"
            :id="id || null"
            v-model="localValue"
            :disabled="disabled"
            @change="onChange"
            ref="input"
    >
        <option v-for="option in formOptions"
                :value="option.value"
                v-html="option.text"
                :disabled="option.disabled"
        ></option>
    </select>
</template>

<script>
    import formOptions from '../mixins/form-options';
    import formMixin from '../mixins/form';

    export default {
        mixins: [formMixin, formOptions],
        data() {
            return {
                localValue: this.value
            };
        },
        methods: {
            onChange: function() {
                this.$emit('change', localValue);
            }
        },
        props: {
            value: {},
            options: {
                type: [Array, Object],
                required: true
            },
            returnObject: {
                type: Boolean,
                default: false
            }
        }
    };

</script>
