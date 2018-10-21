<script>
import VueChart from 'vue-chartjs'

export default {
  extends: VueChart.Line,
  props: ['chartData'],
  mixins: [VueChart.mixins.reactiveProp],
  mounted () {
    window.Chart.defaults.global.defaultFontColor = 'rgba(210, 210, 210, 0.9)'
    window.Chart.defaults.global.defaultColor = 'rgba(210, 210, 210, 0.9)'

    this.renderChart(this.chartData, {
      legend: {
        display: false
      },
      scales: {
				xAxes: [{
					type: 'time',
					display: true,
					scaleLabel: {
						display: false
					},
					ticks: {
						major: {
							fontStyle: 'bold',
							fontColor: '#FF0000'
						}
					}
				}],
				yAxes: [{
					display: true,
					scaleLabel: {
						display: true,
						labelString: 'Your Balance'
					}
				}]
			}
    })
  }
}
</script>

<style>
</style>
