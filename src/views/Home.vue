<template>
  <div class="home">
    <div>
      <img alt="Vue logo" src="../assets/logo.png">
      <hr>
      <h1>Web components(Vue wrapper)</h1>
      <wc-my-component msg="Vue web component wrapper"></wc-my-component>
      <wc-hello-world></wc-hello-world>
      <wc-sc-input></wc-sc-input>
      <wc-sc-select placeholder="select wc" @input="getSelectEvt($event)" v-model="selectedVal">
        <option value="flint">Flint</option>
        <option value="silver">Silver</option>
      </wc-sc-select>
    </div>
    <router-link to="/app2/about">App2's about page</router-link>
    <br/>
    <router-link to="/app3">app3 inside</router-link>
  </div>
</template>

<script>
// @ is an alias to /src
import { createNamespacedHelpers } from 'vuex';
import HelloWorld from '@/components/HelloWorld.vue';

const { mapGetters, mapActions } = createNamespacedHelpers('app1');

export default {
  name: 'home',
  data() {
    return {
      selectedVal: '',  
    };
  },
  computed: {
    ...mapGetters([
      'getStoreApp1',
    ]),
  },
  methods: {
    ...mapActions([
      'updateStoreApp1',
    ]),
    getSelectEvt(evt) {
      console.log('selecionouuu', evt);
    },
  },
  mounted() {
    this.updateStoreApp1();
    this.$store.dispatch('app2/updateStoreApp2');
  },
  components: {
    HelloWorld
  }
}
</script>
