<template>
  <div ref="vega" :mode="mode"></div>
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
    },

    props: {
      mode: String
    },

    watch: {
      mode (m) {
        console.log(m);
      }
    },
  };
</script>
