<template>
  <van-datetime-picker
    :value="new Date(value)"
    :type="type"
    :min-date="formModel.rules.minDate"
    :max-date="formModel.rules.maxDate"
    :show-toolbar="showToolbar"
    @confirm="__confirm"
    @cancel="__cancel"
    @change="!showToolbar && __change($event)"
  />
</template>

<script>
import { DatetimePicker } from 'vant'
import mixin from './mixin'
export default {
  name: 'VDatetimePicker',

  components: {
    [DatetimePicker.name]: DatetimePicker
  },

  mixins: [mixin],

  methods: {
    _format(value) {
      const currentFormat = Array.isArray(value)
        ? this.datejs(new Date(...value))
        : this.datejs(new Date(value))
      let innerValue = ''
      if (this.type === 'year-month') {
        innerValue = currentFormat.format('yyyy-MM')
      } else if (this.type === 'date') {
        innerValue = currentFormat.format('yyyy-MM-dd')
      } else {
        innerValue = currentFormat.format('yyyy-MM-dd HH:mm')
      }
      return {
        innerValue,
        value: this.formModel.rules.valueFormat
          ? this.formModel.rules.valueFormat === 'timestamp'
            ? new Date(value).getTime()
            : currentFormat.format(this.formModel.rules.valueFormat)
          : value
      }
    }
  }
}
</script>
