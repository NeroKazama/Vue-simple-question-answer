<template>
  <div class="container">
    <component
      :is="screens[position]"
      :question="question"
      :result="result"
      @goto="handleGoto"
      @question="handleQuestion"
      @showResult="showResult"
      @startOver="startOver"
      @handleToast="handleToast"
    />
  </div>
</template>

<script>
import appInitial from './components/IniComponent.vue'
import appConfirm from './components/ConfirmComponent.vue'
import appResults from './components/ResultsComponent.vue'

export default {
  components: {
    appInitial,
    appConfirm,
    appResults
  }, 

  data() {
    return {
      list: [
        "Yes",
        "No",
        "Maybe",
        "Not sure..try again",
        "Ask a friend",
        "Call the police",
      ],
      screens:['appInitial', 'appConfirm', 'appResults'],
      position:0,
      question:'',
      result:''
    }
  },

  methods: {
    handleToast(value) {
      this.$toast.show(value.message, {
        type: value.type,
        position:"top",
        duration: 2000,
        pauseOnHover:false
      })
    },

    handleGoto(pos) {
      this.position = pos
    },

    handleQuestion(q) {
      this.question = q
    },

    getRandomValue() {
      return this.list[Math.floor(Math.random() * this.list.length)] 
    },

    randomResult() {
      let rand = this.getRandomValue();

      if(this.result !== ''){
          while (rand === this.result){
            rand = this.getRandomValue();
          }
      }
      this.result = rand;
    },

    showResult() {
      this.randomResult();
    },

    startOver(){
        this.position = 0;
        this.question = "";
        this.result = "";
    }
  }
}

</script>

<style>
  @import './assets/style.css';

</style>
