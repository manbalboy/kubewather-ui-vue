<template>
  <div class="row">
    <!-- Big Chart -->
    <div class="col-12">
      <card type="chart">
        <template slot="header">
          <div class="row">
            <div class="col-sm-6" :class="isRTL ? 'text-right' : 'text-left'">
              <h5 class="card-category">Total shipments</h5>
              <h2 class="card-title">Performance</h2>
            </div>
            <div class="col-sm-6 d-flex d-sm-block">
              <div
                class="btn-group btn-group-toggle"
                :class="isRTL ? 'float-left' : 'float-right'"
                data-toggle="buttons"
              >
                <label
                  v-for="(option, index) in bigLineChartCategories"
                  :id="index"
                  :key="option.name"
                  class="btn btn-sm btn-primary btn-simple"
                  :class="{ active: bigLineChart.activeIndex === index }"
                >
                  <input
                    type="radio"
                    name="options"
                    autocomplete="off"
                    :checked="bigLineChart.activeIndex === index"
                    @click="initBigChart(index)"
                  />
                  <span class="d-none d-sm-block">{{ option.name }}</span>
                  <span class="d-block d-sm-none">
                    <i :class="option.icon"></i>
                  </span>
                </label>
              </div>
            </div>
          </div>
        </template>
        <div class="chart-area">
          <LineChart
            ref="bigChart"
            style="height: 100%"
            :chart-data="bigLineChart.chartData"
            :gradient-colors="bigLineChart.gradientColors"
            :gradient-stops="bigLineChart.gradientStops"
            :extra-options="bigLineChart.extraOptions"
          >
          </LineChart>
        </div>
      </card>
    </div>
    <!-- Stats Cards -->
    <div v-for="card in statsCards" :key="card.title" class="col-lg-3 col-md-6">
      <StatsCard :title="card.title" :sub-title="card.subTitle" :type="card.type" :icon="card.icon">
        <div slot="footer" v-html="card.footer"></div>
      </StatsCard>
    </div>

    <!-- Small charts -->
    <div class="col-lg-4" :class="{ 'text-right': isRTL }">
      <card type="chart">
        <template slot="header">
          <h5 class="card-category">Total Shipments</h5>
          <h3 class="card-title"> <i class="tim-icons icon-bell-55 text-primary"></i> 763,215 </h3>
        </template>
        <div class="chart-area">
          <LineChart
            style="height: 100%"
            :chart-data="purpleLineChart.chartData"
            :gradient-colors="purpleLineChart.gradientColors"
            :gradient-stops="purpleLineChart.gradientStops"
            :extra-options="purpleLineChart.extraOptions"
          >
          </LineChart>
        </div>
      </card>
    </div>
    <div class="col-lg-4" :class="{ 'text-right': isRTL }">
      <card type="chart">
        <template slot="header">
          <h5 class="card-category">Daily Sales</h5>
          <h3 class="card-title"> <i class="tim-icons icon-delivery-fast text-info"></i> 3,500€ </h3>
        </template>
        <div class="chart-area">
          <BarChart
            style="height: 100%"
            :chart-data="blueBarChart.chartData"
            :gradient-stops="blueBarChart.gradientStops"
            :extra-options="blueBarChart.extraOptions"
          >
          </BarChart>
        </div>
      </card>
    </div>
    <div class="col-lg-4" :class="{ 'text-right': isRTL }">
      <card type="chart">
        <template slot="header">
          <h5 class="card-category">Completed tasks</h5>
          <h3 class="card-title"> <i class="tim-icons icon-send text-success"></i> 12,100K </h3>
        </template>
        <div class="chart-area">
          <LineChart
            style="height: 100%"
            :chart-data="greenLineChart.chartData"
            :gradient-stops="greenLineChart.gradientStops"
            :extra-options="greenLineChart.extraOptions"
          >
          </LineChart>
        </div>
      </card>
    </div>
    <div class="col-lg-5">
      <card type="tasks" :header-classes="{ 'text-right': isRTL }">
        <template slot="header">
          <h6 class="title d-inline">Tasks (5)</h6>
          <p class="card-category d-inline">Today</p>
          <BaseDropdown
            menu-on-right=""
            tag="div"
            title-classes="btn btn-link btn-icon"
            :class="{ 'float-left': isRTL }"
          >
            <i slot="title" class="tim-icons icon-settings-gear-63"></i>
            <a class="dropdown-item" href="#pablo"> Action </a>
            <a class="dropdown-item" href="#pablo"> Another action </a>
            <a class="dropdown-item" href="#pablo"> Something else </a>
          </BaseDropdown>
        </template>
        <div class="table-full-width table-responsive">
          <TaskList></TaskList>
        </div>
      </card>
    </div>
    <div class="col-lg-7">
      <card class="card" :header-classes="{ 'text-right': isRTL }">
        <h5 slot="header" class="card-title">Management table</h5>
        <div class="table-responsive"><UserTable></UserTable></div>
      </card>
    </div>
    <div class="col-lg-12"><CountryMapCard></CountryMapCard></div>
  </div>
</template>
<script>
  import LineChart from '@/components/Charts/LineChart';
  import BarChart from '@/components/Charts/BarChart';
  import * as chartConfigs from '@/components/Charts/config';
  import TaskList from '@/components/Dashboard/TaskList';
  import UserTable from '@/components/Dashboard/UserTable';
  import CountryMapCard from '@/components/Dashboard/CountryMapCard';
  import StatsCard from '@/components/Cards/StatsCard';
  import config from '@/config';
  import DashboardNavbar from '@/components/Layout/DashboardNavbar.vue';

  const bigChartData = [
    [100, 70, 90, 70, 85, 60, 75, 60, 90, 80, 110, 100],
    [80, 120, 105, 110, 95, 105, 90, 100, 80, 95, 70, 120],
    [60, 80, 65, 130, 80, 105, 90, 130, 70, 115, 60, 130],
  ];
  const bigChartLabels = ['JAN', 'FEB', 'MAR', 'APR', 'MAY', 'JUN', 'JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'];
  const bigChartDatasetOptions = {
    fill: true,
    borderColor: config.colors.primary,
    borderWidth: 2,
    borderDash: [],
    borderDashOffset: 0.0,
    pointBackgroundColor: config.colors.primary,
    pointBorderColor: 'rgba(255,255,255,0)',
    pointHoverBackgroundColor: config.colors.primary,
    pointBorderWidth: 20,
    pointHoverRadius: 4,
    pointHoverBorderWidth: 15,
    pointRadius: 4,
  };

  export default {
    name: 'Dashboard',
    components: {
      LineChart,
      BarChart,
      StatsCard,
      TaskList,
      CountryMapCard,
      UserTable,
      DashboardNavbar,
    },
    // asyncData() {},

    // async asyncData(context) {
    //   console.log(process.env.TEST_ENV);
    //   // eslint-disable-next-line nuxt/no-timing-in-fetch-data
    //   const wait = _ => new Promise(resolve => setTimeout(resolve, 10000));
    //   await wait();
    //   console.log('---------------------------------------------');
    //   return {
    //     test: 1,
    //   };
    // },

    data() {
      return {
        statsCards: [
          {
            title: '150GB',
            subTitle: 'Number',
            type: 'warning',
            icon: 'tim-icons icon-chat-33',
            footer: '<i class="tim-icons icon-refresh-01"></i> Update Now',
          },
          {
            title: '+45K',
            subTitle: 'Followers',
            type: 'primary',
            icon: 'tim-icons icon-shape-star',
            footer: '<i class="tim-icons icon-sound-wave"></i></i> Last Research',
          },
          {
            title: '150,000',
            subTitle: 'Users',
            type: 'info',
            icon: 'tim-icons icon-single-02',
            footer: '<i class="tim-icons icon-trophy"></i> Customer feedback',
          },
          {
            title: '23',
            subTitle: 'Errors',
            type: 'danger',
            icon: 'tim-icons icon-molecule-40',
            footer: '<i class="tim-icons icon-watch-time"></i> In the last hours',
          },
        ],
        bigLineChart: {
          activeIndex: 0,
          chartData: {
            datasets: [
              {
                ...bigChartDatasetOptions,
                data: bigChartData[0],
              },
            ],
            labels: bigChartLabels,
          },
          extraOptions: chartConfigs.purpleChartOptions,
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
          categories: [],
        },
        purpleLineChart: {
          extraOptions: chartConfigs.purpleChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'],
            datasets: [
              {
                label: 'Data',
                fill: true,
                borderColor: config.colors.primary,
                borderWidth: 2,
                borderDash: [],
                borderDashOffset: 0.0,
                pointBackgroundColor: config.colors.primary,
                pointBorderColor: 'rgba(255,255,255,0)',
                pointHoverBackgroundColor: config.colors.primary,
                pointBorderWidth: 20,
                pointHoverRadius: 4,
                pointHoverBorderWidth: 15,
                pointRadius: 4,
                data: [80, 100, 70, 80, 120, 80],
              },
            ],
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.2, 0],
        },
        greenLineChart: {
          extraOptions: chartConfigs.greenChartOptions,
          chartData: {
            labels: ['JUL', 'AUG', 'SEP', 'OCT', 'NOV'],
            datasets: [
              {
                label: 'My First dataset',
                fill: true,
                borderColor: config.colors.danger,
                borderWidth: 2,
                borderDash: [],
                borderDashOffset: 0.0,
                pointBackgroundColor: config.colors.danger,
                pointBorderColor: 'rgba(255,255,255,0)',
                pointHoverBackgroundColor: config.colors.danger,
                pointBorderWidth: 20,
                pointHoverRadius: 4,
                pointHoverBorderWidth: 15,
                pointRadius: 4,
                data: [90, 27, 60, 12, 80],
              },
            ],
          },
          gradientColors: ['rgba(66,134,121,0.15)', 'rgba(66,134,121,0.0)', 'rgba(66,134,121,0)'],
          gradientStops: [1, 0.4, 0],
        },

        blueBarChart: {
          extraOptions: chartConfigs.barChartOptions,
          chartData: {
            labels: ['USA', 'GER', 'AUS', 'UK', 'RO', 'BR'],
            datasets: [
              {
                label: 'Countries',
                fill: true,
                borderColor: config.colors.info,
                borderWidth: 2,
                borderDash: [],
                borderDashOffset: 0.0,
                data: [53, 20, 10, 80, 100, 45],
              },
            ],
          },
          gradientColors: config.colors.primaryGradient,
          gradientStops: [1, 0.4, 0],
        },
      };
    },
    computed: {
      enableRTL() {
        return this.$route.query.enableRTL;
      },
      isRTL() {
        return this.$rtl.isRTL;
      },
      bigLineChartCategories() {
        return [
          { name: 'Accounts', icon: 'tim-icons icon-single-02' },
          {
            name: 'Purchases',
            icon: 'tim-icons icon-gift-2',
          },
          { name: 'Sessions', icon: 'tim-icons icon-tap-02' },
        ];
      },
    },
    mounted() {
      console.log('mounted====', process);
      // this.$nextTick(() => {
      //   this.$nuxt.$loading.start();
      //   setTimeout(() => {
      //     this.$nuxt.$loading.finish();
      //   }, 5000);
      // });
      this.initBigChart(0);
    },
    methods: {
      delay() {
        return new Promise(resolve => setTimeout(resolve(1), 70000));
      },
      initBigChart(index) {
        const chartData = {
          datasets: [
            {
              ...bigChartDatasetOptions,
              data: bigChartData[index],
            },
          ],
          labels: bigChartLabels,
        };
        this.$refs.bigChart.updateGradients(chartData);
        this.bigLineChart.chartData = chartData;
        this.bigLineChart.activeIndex = index;
      },
    },
  };
</script>
<style></style>
