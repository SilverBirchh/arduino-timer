<template>
  <div>
    <h1>Stats</h1>
    <p>
      Your 10 individual session times (seconds): {{contact}}
    </p>
    <p>
      Your average session time is (seconds): {{avg}}
    </p>
    <div class="chart-container">ı
      <canvas id="myChart" width="100" height="100"></canvas>
    </div>

  </div>
</template>

<script>
import Chart from 'chart.js';

export default {
	name: 'ArdunioHistory',
	data: function() {
		return {
			contact: [],
			avg: 0,
		};
	},
	mounted: async function() {
		let res = await fetch('http://localhost:8000/history');
		res = await res.json();
		this.contact = res.slice(Math.max(res.length - 10, 1));
		const labels = new Array(10).fill(0).map((r, i) => i);

		var ctx = document.getElementById('myChart').getContext('2d');
		var myChart = new Chart(ctx, {
			type: 'bar',
			data: {
				labels: labels,
				datasets: [
					{
						label: '10 Last Individual Session Times',
						data: this.contact,
						backgroundColor: '#2196F3',
						hoverBackgroundColor: '#03A9F4',
					},
				],
			},
			options: {
				scales: {
					yAxes: [
						{
							ticks: {
								beginAtZero: true,
							},
						},
					],
				},
			},
		});

		const sum = this.contact.reduce((a, b) => a + b, 0);
		this.avg = sum / this.contact.length;
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.chart-container {
	position: relative;
	margin: auto;
	height: 30vh;
	width: 80%;
}
</style>
