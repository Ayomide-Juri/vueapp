<template>
  <div class="Skills">
   <h3>Welcome Enter Your Skills</h3>


   <div class="container">


    <form @submit.prevent="addSkill">
    <input type="text" placeholder="Enter a skill you have.."  v-model="skill" v-validate="'min:5'" name="skill"> 


       <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
      </transition>
    </form>




     <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
       <li v-for="(data, index) in skills" :key='index'>{{data.skill}}</li>
       </transition-group>
           <p v-if="skills.length >= 2">!!Nice this are the Skills you possess</p>
       <p v-else>Welcome Update Your Skills</p>
     </ul>
   </div>

  
  </div>
</template>










<script>
export default {
  name: "Skills",
  data() {
    return {
      skill: "",

      skills: []
    };
  },

  methods: {
    addSkill() {
      this.$validator.validateAll().then(result => {
        if (result) {
          this.skills.push({ skill: this.skill });
          this.skill = "";
        } else {
          console.log("Not valid");
        }
      });
    }
  },
  remove(id) {
    this.skills.splice(id, 1);
  }
};
</script>











<!-- Add "scoped" attribute to limit CSS to this component only -->
<style src="./Skills.css" scoped>
</style>
