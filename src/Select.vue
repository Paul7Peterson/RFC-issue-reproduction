<script setup lang="ts" generic="VueGen extends AppSelectOption<string | number>">
  import { defineProps, defineEmits } from 'vue';
  
  export interface AppSelectOption<T extends string | number> {
    value: T;
    text: string;
    disabled?: boolean;
  }

  export interface Props<T extends AppSelectOption<string | number>> {
    text: string;
    modelValue: T['value'] | undefined;
    options: readonly T[];
    disabled?: boolean;
  }

  defineProps<Props<VueGen>>();

  const emits = defineEmits<{
    (e: 'update:modelValue', modelValue: VueGen['value']): void;
  }>();

  function onChange (e: Event): void {
    const target = e.target as HTMLSelectElement;
    emits('update:modelValue', target.value);
  }
</script>

<template>
  <label>
    {{ text }}
    <select
      :value="modelValue"
      :disabled="disabled"
      @change="onChange"
    >
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
        :disabled="option.disabled"
      >
        {{ option.text }}
      </option>
    </select>
  </label>
</template>