
<template>
  <button @click="increment"> mapGetter read from the start: {{count1}}</button>
  <br />
  <br />
  <button v-if="!hasRegisteredModule" @click="registerModule">Register my module</button>
  <div v-if="hasRegisteredModule"> Module registered</div>
  <br />
  <div v-if="hasRegisteredModule"> mapGetter first read after registration of module : {{count2}}</div>
</template>

<script>
import { mapGetters, mapMutations } from 'vuex';
import myDynamicModule from './store/dynamicModule.js';

export default {
	name: 'App',
  data() {
		return {
			hasRegisteredModule: false
		};
	},
  computed: {
    ...mapGetters({count1: 'count', count2: 'count'}),
  },
  methods: {
    ...mapMutations(['increment']),
    registerModule(){
      this.$store.registerModule(myDynamicModule.name, myDynamicModule);
      this.hasRegisteredModule = true;
    },
  }
};
</script>
