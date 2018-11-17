<template>
<div>
  <h1>Are you moving enough?</h1>
  <h2>Time since last break: {{ time | formatTime }}</h2>

  <p>
    It's recommended to take a break every hour.<br /> Once you start work we'll notify you when it's time to take a break.<br />However, feel free to change the minutes between breaks using this handy slider.
  </p>
  <vue-slider ref="slider" v-model="breakTime" v-bind="options"></vue-slider>
</div>
</template>

<script>
const numeral = require('numeral');
import vueSlider from 'vue-slider-component';

export default {
	name: 'ArdunioTime',
	components: {
		vueSlider,
	},
	data: function() {
		return {
			time: 0,
			breakTime: 60,
			options: {
				eventType: 'auto',
				height: 20,
				dotSize: 20,
				min: 0,
				max: 120,
				interval: 1,
				show: true,
				speed: 1,
				tooltipDir: 'bottom',
				lazy: true,
			},
		};
	},
	beforeCreate: function() {
		//_------------------------
		const ws = new WebSocket('ws://localhost:40510');

		ws.onopen = function() {
			console.log('Websocket is connected ...');
			ws.send('connected');
		};

		// ----------

		ws.onmessage = ev => {
			if (ev.data !== 'MAKE_SOUND') {
				this.time = ev.data ? ev.data : 0;
			} else {
				const notification = new Notification('Time to move around!');
			}
		};
	},
	mounted: function() {
		this.setUpNotification();
	},
	watch: {
		// whenever breakTime changes, this function will run
		breakTime: function(breakTime) {
			console.log(breakTime);
			const data = { breakTime: breakTime };
			fetch('http://localhost:8000/breakTime', {
				method: 'POST',
				body: JSON.stringify(data),
			})
				.then(() => console.log('Time Updated'))
				.catch(err => console.log(err));
		},
	},
	methods: {
		setUpNotification: function() {
			// Need to ask the user for permission
			if (
				Notification.permission === 'denied' ||
				Notification.permission === 'default'
			) {
				Notification.requestPermission(function(permission) {
					// If the user accepts, let's create a notification
					if (permission === 'granted') {
						const notification = new Notification(
							"You've now set up notifications"
						);
					}
				});
			}
		},
	},
	filters: {
		formatTime: function(value) {
			value = +value;
			if (!isNaN(value)) {
				if (value === 0) {
					return 'No presence detected';
				} else {
					return numeral(value).format('00:00:00');
				}
			}
			return value;
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
	margin: 40px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: inline-block;
	margin: 0 10px;
}
a {
	color: #42b983;
}
</style>
