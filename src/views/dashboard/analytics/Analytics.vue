<template>
  <section id="dashboard-analytics">
    <b-row class="match-height">
      <b-col
        lg="6"
        md="12"
      >
        <analytics-congratulation :data="data.congratulations" />
      </b-col>
      <b-col
        lg="6"
        sm="6"
      >
        <statistic-card-with-area-chart
          v-if="data.subscribersGained"
          icon="StarIcon"
          :statistic="kFormatter(data.subscribersGained.analyticsData.subscribers)"
          statistic-title="Puntos acumulados"
          :chart-data="data.subscribersGained.series"
        />
      </b-col>
    </b-row>

    <b-row class="match-height">
      <b-col lg="6">
        <ChartjsBarChart />
        <!--        <analytics-avg-sessions :data="data.avgSessions" />-->
      </b-col>
      <b-col lg="6">
        <b-card no-body>
          <b-card-body>
            <b-card-title>Canción recomendada</b-card-title>
            <b-card-sub-title>El botón del pantalón - Systema solar</b-card-sub-title>
          </b-card-body>
          <b-img
            fluid
            width="320"
            style="margin: auto"
            :src="require('@/assets/images/elements/systemaSolar.jpg')"
            alt="Card image cap"
          />
          <b-card-body>
            <b-card-text><i>"Ando por la vida relajao y feliz..."</i></b-card-text>
            <b-link class="card-link" href="https://www.youtube.com/watch?v=rLJSMn5Mc2U" target="_blank">
              Escuchar ahora
            </b-link>
          </b-card-body>
        </b-card>
        <!--        <analytics-support-tracker :data="data.supportTracker" />-->
      </b-col>
    </b-row>

    <b-row class="match-height">
      <b-col lg="4">
<!--        <analytics-timeline :data="data.timeline" />-->
        <CardAdvanceMeetup></CardAdvanceMeetup>
      </b-col>
      <b-col lg="8">
        <analytics-sales-radar-chart :data="data.salesChart" />
      </b-col>
    </b-row>

    <!--    <b-row>
      <b-col cols="12">
        <invoice-list />
      </b-col>
    </b-row>-->
  </section>
</template>

<script>
import {
  BRow, BCol, BCard, BCardText, BCardBody, BCardTitle, BCardSubTitle, BLink, BImg,
} from 'bootstrap-vue'

import StatisticCardWithAreaChart from '@core/components/statistics-cards/StatisticCardWithAreaChart.vue'
import { kFormatter } from '@core/utils/filter'
// import InvoiceList from '@/views/apps/invoice/invoice-list/InvoiceList.vue'
import AnalyticsCongratulation from './AnalyticsCongratulation.vue'
// import AnalyticsAvgSessions from './AnalyticsAvgSessions.vue'
// import AnalyticsSupportTracker from './AnalyticsSupportTracker.vue'
// import AnalyticsTimeline from './AnalyticsTimeline.vue'
import AnalyticsSalesRadarChart from './AnalyticsSalesRadarChart.vue'
import ChartjsBarChart from '../../charts-and-maps/charts/chartjs/ChartjsBarChart.vue'
import CardAdvanceMeetup from '../../card/card-advance/CardAdvanceMeetup.vue'

export default {
  components: {
    BCard,
    BCardText,
    BCardBody,
    BCardTitle,
    BCardSubTitle,
    BLink,
    BImg,
    BRow,
    BCol,
    AnalyticsCongratulation,
    StatisticCardWithAreaChart,
    AnalyticsSalesRadarChart,
    ChartjsBarChart,
    CardAdvanceMeetup,
  },
  data() {
    return {
      data: {},
    }
  },
  created() {
    // data
    this.$http.get('/analytics/data')
      .then(response => { this.data = response.data })
  },
  methods: {
    kFormatter,
  },
}
</script>
