<template>
  <div class="Timer">
    <ArdunioTime />
  </div>
</template>


<script>
// @ is an alias to /src
import ArdunioTime from '@/components/ArdunioTime.vue';

export default {
	name: 'timer',
	components: {
		ArdunioTime,
	},
};
</script>
