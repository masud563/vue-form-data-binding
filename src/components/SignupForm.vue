<template>
  <form class="form">
    <label for="email" >EMAIL:</label>
    <input type="email" v-model="email">

    <label for="password" >PASSWORD:</label>
    <input type="password" v-model="password">

    <select v-model="role">
      <option value="designer">Web Designer</option>
      <option value="developer">Web Developer</option>
    </select>

    <div>
      <input type="checkbox" v-model="term">
      <label>ACCEPT TERMS AND CONDITIONS</label>
    </div>

    <div>
      <label>SKILLS:</label>
      <input type="text" @keyup="addSkill" v-model="tempSkill">
    </div>

    <div v-for="skill in skills" >
      <p>{{ skill }}</p>
    </div>

  </form>

  <p>Email: {{email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Term: {{ term }}</p>
  <p>Skills: {{skills}}</p>

</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'developer',
      term: false,
      tempSkill: '',
      skills: []
    }
  },

  methods: {
    addSkill(e) {
      console.log(e)
      if(e.key === ',' && this.tempSkill){
        this.tempSkill =this.tempSkill.replace(',','')
        if(!this.skills.includes(this.tempSkill)){
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
      }
      
    }
  }
}
</script>

<style>
  .form {
    width: 420px;
    background-color: white;
    margin: 30px auto;
    border-radius: 10px;
    padding: 40px;
    text-align: left;
  }
  .form label {
    font-weight: bold;
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    letter-spacing: 1px;
    font-size: 0.6em;
  }
  .form input,select {
    display: block;
    padding: 10px 6px;
    box-sizing: border-box;
    width: 100%;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
  .form input[type="checkbox"] {
    display: inline-block;
    position: relative;
    top: 2px;
    width: 16px;
    margin-right: 10px;
  }
</style>