<script setup>
  const props = defineProps({
    categoryId: Number,
    noText: Boolean,
  });
  
  const isChecked = ref(true);
  defineEmits(['toggle']);

  const currentCategory = categories.find(cat => cat.id === props.categoryId);
  const { id, name, color } = currentCategory;
  const displayName = props.noText ? '' : name;

</script>

<template>
  <label
    class="tag"
    :style="`background-color: var(--c-${color})`"
    :disabled="!isChecked"
    @change="$emit('toggle', categoryId, $event.target.checked)"
  >
    <input
      type="checkbox"
      :checked="isChecked"
      v-model="isChecked"
    />
    <span>
      {{ displayName }}
    </span>
  </label>
  
</template>

<style>
  .tag {
    display: inline-block;
    font-size: 1rem;
    color: var(--c-gray-200);
    border: none;
    border-radius: 100rem;
    padding: .25rem .85rem;
    margin: .25rem;
    min-height: 1rem;
    cursor: pointer;
  }

  .tag[disabled='true'] {
    opacity: .5;
  }

  .tag input {
    display: none;
  }
</style>