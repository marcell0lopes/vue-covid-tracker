<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow-md bg-slate-700 p-10 text-center rounded text-white/95">
      <h3 class="text-2xl font-bold mb-4">Cases</h3>
      <div class="text-lg mb-4">
        <h4 class="font-bold mb-2">
          New:
          <span class="font-normal text-emerald-500">{{
            formatNumber(stats.NewConfirmed)
          }}</span>
        </h4>

        <h4 class="font-bold">
          Total:
          <span class="font-normal text-emerald-500">{{
            formatNumber(stats.TotalConfirmed)
          }}</span>
        </h4>
      </div>
    </div>

    <div class="shadow-md bg-slate-900 p-10 text-center rounded text-white/95">
      <h3 class="text-2xl font-bold mb-4">Deaths</h3>
      <div class="text-lg mb-4">
        <h4 class="font-bold mb-2">
          New:
          <span class="font-normal text-emerald-500">{{
            formatNumber(stats.NewDeaths)
          }}</span>
        </h4>

        <h4 class="font-bold">
          Total:
          <span class="font-normal text-emerald-500">{{
            formatNumber(stats.TotalDeaths)
          }}</span>
        </h4>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DataCard',
  props: ['stats'],
  methods: {
    formatNumber(number) {
      return number.toLocaleString('pt-BR');
    },
  },
};
</script>
