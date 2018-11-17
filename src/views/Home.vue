<template>
  <div class="home">
    <img src="../assets/arduino.png">
    <ArdunioHome msg='Ardunio Eye Health'/>
  </div>
</template>

<script>
// @ is an alias to /src
import ArdunioHome from '@/components/ArdunioHome.vue';

export default {
	name: 'home',
	components: {
		ArdunioHome,
	},
};
</script>

<style scoped lang="scss">
img {
	width: 20%;
}
</style>
