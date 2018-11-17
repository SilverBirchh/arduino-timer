<template>
  <div class="History">
    <ArdunioHistory />
  </div>
</template>


<script>
// @ is an alias to /src
import ArdunioHistory from '@/components/ArdunioHistory.vue';

export default {
	name: 'history',
	components: {
		ArdunioHistory,
	},
};
</script>
