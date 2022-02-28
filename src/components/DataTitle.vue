<template>
  <div class="text-center flex flex-row items-center justify-center mb-6">
    <h2 class="inline text-3xl font-bold text-gray-900">
      {{ text }}
    </h2>
    <span class="font-normal text-sm mx-4 text-gray-500">
      ({{ timestamp }})
    </span>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'DataTitle',
  props: ['text', 'dataDate'],
  computed: {
    timestamp: function () {
      return moment(this.dataDate).format('h:mm A, Do MMMM YYYY');
    },
  },
};
</script>
