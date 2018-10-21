<script>
import { Line, mixins } from 'vue-chartjs'

export default {
  extends: Line,
  mixins: [mixins.reactiveProp],
  props: ['chartData', 'options'],
  mounted () {
    window.Chart.defaults.global.defaultFontColor = 'rgba(210, 210, 210, 0.9)';
    window.Chart.defaults.global.defaultColor = 'rgba(210, 210, 210, 0.9)';
    this.renderChart(this.chartData, this.options)
  }
}
</script>

<style>
</style>
