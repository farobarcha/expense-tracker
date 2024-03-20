<template>
  <div class="income-period inc-exp-container">
    <h4>Select Period</h4>
    <datepicker
      placeholder="Select Month"
      :value="defaultValue"
      :minimum-view="'month'"
      :maximum-view="'month'"
      :disabled-dates="disabledDates"
      @changedMonth="handleChangedMonth"
      @input="selectedDate"
      iconColor="red"
      iconHeight="18"
      iconWidth="18"
      full-month-name="true"
    ></datepicker>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Datepicker from "vuejs3-datepicker";

const props = defineProps({
    currentYear: {
        type: Number
    },
    currentMonth: {
        type: Number
    },
})

const emit = defineEmits('loadPeriod');
const defaultValue = ref(new Date(props.currentYear, props.currentMonth));

const handleChangedMonth = (payload) => {
  emit('loadCurrentPeriod', payload.timestamp);
};

const disabledDates =  {
  from: new Date(new Date().getFullYear(), new Date().getMonth(), 1),
  preventDisableDateSelection: true
}
</script>