<template>
  <div ref="vega"></div>
</template>

<script>
  import { parse, View } from 'vega';
  import spec from '@/assets/spec.vg.json';

  export default {
    mounted () {
      this.vega = new View(parse(spec))
        .initialize(this.$refs.vega)
        .renderer('svg')
        .run();
    }
  };
</script>
