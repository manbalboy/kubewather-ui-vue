<template>
  <div class="table-shopping">
    <ElTable style="width: 100%" :data="productsTable">
      <ElTableColumn min-width="140">
        <div slot-scope="{ row }" class="img-container">
          <img :src="row.image" alt="product image" />
        </div>
      </ElTableColumn>

      <ElTableColumn min-width="270" label="Product">
        <div slot-scope="{ row }" class="td-name">
          <a href="#jacket">{{ row.title }}</a> <br />
          <small>{{ row.description }}</small>
        </div>
      </ElTableColumn>
      <ElTableColumn min-width="120" label="Color" prop="color"></ElTableColumn>
      <ElTableColumn min-width="100" label="Size" prop="size"></ElTableColumn>
      <ElTableColumn min-width="100" label="Price" align="center">
        <template slot-scope="{ row }"> <small>€</small> {{ row.price }} </template>
      </ElTableColumn>
      <ElTableColumn min-width="160" label="QTY" align="center">
        <template slot-scope="{ row }">
          <div class="btn-group">
            <base-button type="info" class="btn-simple" size="sm" @click="decreaseQuantity(row)">
              <i class="tim-icons icon-simple-delete"></i>
            </base-button>
            <base-button type="info" size="sm" @click="increaseQuantity(row)">
              <i class="tim-icons icon-simple-add"></i>
            </base-button>
          </div>
          {{ row.quantity }}
        </template>
      </ElTableColumn>
      <ElTableColumn min-width="100" label="Amount" align="right">
        <template slot-scope="{ row }"> <small>€</small> {{ row.amount }} </template>
      </ElTableColumn>
      <ElTableColumn min-width="60" label="" align="left">
        <!--        <template slot-scope="{ row }">-->
        <template>
          <base-button type="primary" class="btn-link">
            <i class="tim-icons icon-simple-remove"></i>
          </base-button>
        </template>
      </ElTableColumn>

      <div slot="append" class="stats-container">
        <div class="stats-total">
          <div class="stats-total-numbers">
            <div class="td-total">Total</div>
            <div class="td-price mr-2"> <small>€</small> {{ shoppingTotal }} </div>
          </div>
        </div>
        <div class="d-flex justify-content-end">
          <base-button type="info" round class="float-right" title="">
            Complete Purchase <i class="tim-icons icon-minimal-right"></i>
          </base-button>
        </div>
      </div>
    </ElTable>
  </div>
</template>

<script>
  import { Table, TableColumn } from 'element-ui';

  export default {
    components: {
      // [Table.name]: Table,
      ElTable: Table,
      // [TableColumn.name]: TableColumn,
      ElTableColumn: TableColumn,
    },
    data() {
      return {
        productsTable: [
          {
            image: 'http://demos.creative-tim.com/nuxt-black-dashboard-pro/img/jacket.png',
            title: 'Suede Biker Jacket ',
            description: 'by Saint Laurent',
            color: 'Black',
            size: 'M',
            price: 3390,
            quantity: 1,
            amount: 3390,
          },
          {
            image: 'http://demos.creative-tim.com/nuxt-black-dashboard-pro/img/t-shirt.png',
            title: 'Jersey T-Shirt',
            description: 'by Balmain',
            color: 'Black',
            size: 'M',
            price: 499,
            quantity: 2,
            amount: 998,
          },
          {
            image: 'http://demos.creative-tim.com/nuxt-black-dashboard-pro/img/gucci.png',
            title: '\tSlim-Fit Swim Short ',
            description: 'by Prada',
            color: 'Red',
            size: 'M',
            price: 200,
            quantity: 1,
            amount: 200,
          },
        ],
      };
    },
    computed: {
      shoppingTotal() {
        return this.productsTable.reduce((accumulator, current) => {
          return accumulator + current.amount;
        }, 0);
      },
    },
    methods: {
      increaseQuantity(row) {
        row.quantity++;
        this.computeAmount(row);
      },
      decreaseQuantity(row) {
        if (row.quantity > 1) {
          row.quantity--;
          this.computeAmount(row);
        }
      },
      computeAmount(row) {
        row.amount = row.quantity * row.price;
      },
    },
  };
</script>
<style scoped>
  .stats-container {
    display: flex;
    flex-direction: column;
    color: rgba(255, 255, 255, 0.7);
    padding-right: 20px;
  }

  .stats-total {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 20px;
  }
  .stats-total-numbers {
    min-width: 240px;
    display: flex;
    justify-content: space-between;
  }
</style>
