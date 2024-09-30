<template>
  <div :class="`input-${type} input-field ${required ? 'required':''} ${error? 'has-error':''}`">
    <label v-if="label" :for="label">{{ label }}</label>
    <input
        v-if="type === 'text' || type === 'email'"
        :id="label"
        :type="type"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
    />

    <textarea
        v-if="type === 'textarea'"
        :id="label"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
    ></textarea>

    <input
        v-if="type === 'checkbox'"
        type="checkbox"
        :checked="modelValue"
        @change="$emit('update:modelValue', $event.target.checked)"
    />


    <!-- Radio buttons with custom label styling -->
    <div v-if="type === 'radio-group'" class="radio-group">
      <label v-for="option in options" :key="option.value" :class="{ 'active': modelValue === option.value }" class="radio-label">
        <input
            type="radio"
            :value="option.value"
            :checked="modelValue === option.value"
            @change="$emit('update:modelValue', option.value)"
        />
        {{ option.label }}
      </label>
    </div>

    <!-- For other input types -->
    <span v-if="error" class="error">{{ error }}</span>
  </div>
</template>

<script>
export default {
  name: "InputField",
  props: {
    label: String,
    modelValue: [String, Boolean],
    type: {
      type: String,
      default: "text",
    },
    value: String, // For radio button value
    options: Array,
    required: Boolean,
    error: String, // Error message
  },
};
</script>

<style scoped>

</style>
