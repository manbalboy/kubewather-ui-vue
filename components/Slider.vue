<template>
  <div class="slider" :class="[`slider-${type}`]" :disabled="disabled"></div>
</template>
<script>
  import noUiSlider from 'nouislider';

  export default {
    name: 'Slider',
    props: {
      value: {
        type: [String, Array, Number],
        description: 'slider value',
      },

      disabled: {
        type: Boolean,
        default: false,
        description: 'whether the slider is disabled',
      },

      start: {
        type: [Number, Array],
        default: 0,
        description: '[noUi Slider start](https://refreshless.com/nouislider/slider-options/#section-start)',
      },

      connect: {
        type: [Boolean, Array],
        default: () => [true, false],
        description: '[noUi Slider connect](https://refreshless.com/nouislider/slider-options/#section-connect)',
      },

      range: {
        type: Object,
        default: () => {
          return {
            min: 0,
            max: 100,
          };
        },
        description: '[noUi Slider range](https://refreshless.com/nouislider/slider-values/#section-range)',
      },

      type: {
        type: String,
        default: '',
        description: 'slider type (color) ',
      },

      options: {
        type: Object,
        default: () => {
          return {};
        },
        description: '[noUi Slider options](https://refreshless.com/nouislider/slider-options/)',
      },
    },
    data() {
      return {
        slider: null,
      };
    },

    watch: {
      value(newValue, oldValue) {
        const slider = this.$el.noUiSlider;
        const sliderValue = slider.get();
        if (newValue !== oldValue && sliderValue !== newValue) {
          if (Array.isArray(sliderValue) && Array.isArray(newValue)) {
            if (oldValue.length === newValue.length && oldValue.every((v, i) => v === newValue[i])) {
              slider.set(newValue);
            }
          } else {
            slider.set(newValue);
          }
        }
      },
    },
    mounted() {
      this.createSlider();
    },

    methods: {
      createSlider() {
        noUiSlider.create(this.$el, {
          start: this.value || this.start,
          connect: this.connect,
          range: this.range,
          ...this.options,
        });

        const slider = this.$el.noUiSlider;

        slider.on('slide', () => {
          const value = slider.get();
          if (value !== this.value) {
            this.$emit('input', value);
          }
        });
      },
    },
  };
</script>
<style></style>
