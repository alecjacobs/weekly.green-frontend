<script>
import VueChart from 'vue-chartjs'
import moment from 'moment'

export default {
  extends: VueChart.Line,
  mounted () {
    Chart.scaleService.updateScaleDefaults('linear', { ticks: { min: 0 }})

    let nextTwoWeeksOfDates = [...Array(14)].map((_, i) => {
      return moment().add(i, 'days').format("dddd")
    })

    let startingBalance = 500

    let nextTwoWeeksOfBalances = [...Array(14)].map((_, i) => {
      return startingBalance + Math.floor(Math.random() * 200)
    })

    this.renderChart({
      labels: nextTwoWeeksOfDates,
      datasets: [
        {
          label: 'Some Data!',
          backgroundColor: '#7af49b',
          data: nextTwoWeeksOfBalances
        }
      ]
    })
  }
}
</script>

<style>
</style>
