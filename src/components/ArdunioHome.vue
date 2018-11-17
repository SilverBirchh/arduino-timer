<template>
  <div>
    <h1>{{ msg }}</h1>
    <p>
      A simple timer to make sure you are keeping<br />
      your eyes healthy and sharp.<br /><br />Taking regular breaks from your computer is important<br />to avoid Computer Vision Syndrome! <br />For more information check out <a rel="noreferrer" target="_blank" href="https://www.specsavers.co.uk/eye-health/computer-eye-strain-symptoms-and-solutions">Specsavers</a>.
    </p>

    <router-link tag="button" to="/timer" class="btn">To the Timer!</router-link>

  </div>
</template>

<script>
export default {
	name: 'ArdunioHome',
	props: {
		msg: String,
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
.btn {
	padding: 10px;
	border-radius: 5px;
	font-size: inherit;
	background-color: #159499;
	color: white;
	border: black;
	cursor: pointer;
	box-shadow: 0px 17px 10px -10px rgba(0, 0, 0, 0.4);

	&:active {
		box-shadow: none;
		margin-top: 3px;
	}
}
</style>
