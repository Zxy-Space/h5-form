<template>
  <div class="v-form-text" @click="__eventHandler('click', formModel)">
    <span
      v-if="!value && formModel.rules.placeholder"
      class="placeholder"
    >
      {{ formModel.rules.placeholder }}
    </span>
    <template v-else>{{ value }}</template>
  </div>
</template>

<script>
import formItemBase from '../mixins/formItemBase'

export default {
  name: 'VText',

  mixins: [formItemBase],

  // eslint-disable-next-line vue/require-prop-types
  props: ['value']
}
</script>
