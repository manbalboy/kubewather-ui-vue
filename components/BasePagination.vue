<template>
  <ul class="pagination" :class="paginationClass">
    <li v-if="showArrows" class="page-item prev-page" :class="{ disabled: value === 1 }">
      <a class="page-link" aria-label="Previous" @click="prevPage">
        <i class="tim-icons icon-double-left" aria-hidden="true"></i>
      </a>
    </li>
    <li v-for="item in range(minPage, maxPage)" :key="item" class="page-item" :class="{ active: value === item }">
      <a class="page-link" @click="changePage(item)">{{ item }}</a>
    </li>
    <li v-if="showArrows" class="page-item page-pre next-page" :class="{ disabled: value === totalPages }">
      <a class="page-link" aria-label="Next" @click="nextPage">
        <i class="tim-icons icon-double-right" aria-hidden="true"></i>
      </a>
    </li>
  </ul>
</template>
<script>
  export default {
    name: 'BasePagination',
    props: {
      /**
       * pagination color type
       */
      type: {
        type: String,
        default: 'primary',
        validator: value => {
          return ['default', 'primary', 'danger', 'success', 'warning', 'info', 'neutral'].includes(value);
        },
      },

      /**
       * page Count
       */
      pageCount: {
        type: Number,
        default: 0,
      },

      /**
       * page 당 숫자
       */
      perPage: {
        type: Number,
        default: 10,
      },

      /**
       * 좌우 arrows visible 여부
       */
      showArrows: {
        type: Boolean,
        default: true,
      },

      /**
       * total
       */
      total: {
        type: Number,
        default: 0,
      },

      /**
       * v-model value
       */
      value: {
        type: Number,
        default: 1,
      },

      /**
       * page 가 보여질 갯수
       */
      pagesToDisplay: {
        type: Number,
        default: 5,
      },
    },
    computed: {
      paginationClass() {
        return `pagination-${this.type}`;
      },

      totalPages() {
        if (this.pageCount > 0) return this.pageCount;
        if (this.total > 0) {
          return Math.ceil(this.total / this.perPage);
        }
        return 1;
      },

      defaultPagesToDisplay() {
        if (this.totalPages > 0 && this.totalPages < this.pagesToDisplay) {
          return this.totalPages;
        }
        return this.pagesToDisplay;
      },

      minPage() {
        if (this.value >= this.defaultPagesToDisplay) {
          const pagesToAdd = Math.floor(this.defaultPagesToDisplay / 2);
          const newMaxPage = pagesToAdd + this.value;

          if (newMaxPage > this.totalPages) {
            return this.totalPages - this.defaultPagesToDisplay + 1;
          }

          return this.value - pagesToAdd;
        } else {
          return 1;
        }
      },

      maxPage() {
        if (this.value >= this.defaultPagesToDisplay) {
          const pagesToAdd = Math.floor(this.defaultPagesToDisplay / 2);
          const newMaxPage = pagesToAdd + this.value;

          if (newMaxPage < this.totalPages) {
            return newMaxPage;
          } else {
            return this.totalPages;
          }
        } else {
          return this.defaultPagesToDisplay;
        }
      },
    },

    watch: {
      perPage() {
        this.$emit('input', 1);
      },
      total() {
        this.$emit('input', 1);
      },
    },

    methods: {
      range(min, max) {
        if (typeof min !== 'number') {
          return [];
        }

        if (typeof max !== 'number') {
          return [];
        }

        if (isNaN(min) || isNaN(max)) {
          throw new TypeError('NaN');
        }

        if (min === Infinity || max === Infinity) {
          throw new TypeError('Infinity');
        }

        const arr = [];
        for (let i = min; i <= max; i++) {
          arr.push(i);
        }
        return arr;
      },

      changePage(item) {
        this.$emit('input', item);
      },

      nextPage() {
        if (this.value < this.totalPages) {
          this.$emit('input', this.value + 1);
        }
      },

      prevPage() {
        if (this.value > 1) {
          this.$emit('input', this.value - 1);
        }
      },
    },
  };
</script>
