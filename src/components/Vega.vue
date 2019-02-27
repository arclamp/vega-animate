<template>
  <div ref="vega" :mode="mode"></div>
</template>

<script>
  import { changeset, parse, View } from 'vega';
  import spec from '@/assets/spec.vg.json';

  function delay (ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }

  export default {
    mounted () {
      this.vega = new View(parse(spec))
        .initialize(this.$refs.vega)
        .renderer('svg')
        .run();

      this.delay = 5;
    },

    props: {
      mode: String
    },

    watch: {
      async mode (mode) {
        switch (mode) {
        case 'low':
          for(let i = 0; i < 68; i++) {
            await this.scaleData(0.99);
            await delay(this.delay);
          }
          break;

        case 'high':
          for(let i = 0; i < 68; i++) {
            await this.scaleData(1.01);
            await delay(this.delay);
          }
          break;

        default:
          throw new Error(`impossible value: ${mode}`);
        }
      }
    },

    methods: {
      async scaleData (m) {
        let data = this.vega.data('source').slice();
        data.forEach(d => {
          d.b *= m;
        });

        const changes = changeset()
          .remove(() => true)
          .insert(data);

        await this.vega.change('source', changes)
          .runAsync();
      }
    }
  };
</script>
