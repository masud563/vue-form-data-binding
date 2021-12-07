<template>
  <form class="form" @submit.prevent="handleSubmit">
    <label for="email" >EMAIL:</label>
    <input type="email" v-model="email" required>

    <label for="password" >PASSWORD:</label>
    <input type="password" v-model="password" required>
    <div class="passwordError" v-if="passwordError">
      <p> {{passwordError }}</p>
    </div>

    <label>Role:</label>
    <select v-model="role">
      <option value="designer">Web Designer</option>
      <option value="developer">Web Developer</option>
    </select>

    <div>
      <label>SKILLS:</label>
      <input type="text" @keyup="addSkill" v-model="tempSkill">
    </div>

    <div v-for="skill in skills" :key="skill" class="pill" @click="removeSkill(skill)" >
      {{ skill }}
    </div>

    <div>
      <input type="checkbox" v-model="term" required>
      <label>ACCEPT TERMS AND CONDITIONS</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

  </form>

  <!-- <p>Email: {{email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Term: {{ term }}</p>
  <p>Skills: {{skills}}</p> -->

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
      skills: [],
      passwordError: ''
    }
  },

  methods: {

    addSkill(e) {
      if(e.key === ',' && this.tempSkill){
        this.tempSkill =this.tempSkill.replace(',','')
        if(!this.skills.includes(this.tempSkill)){
          this.skills.push(this.tempSkill)
        }
        this.tempSkill = ''
      }  
    },

    removeSkill(skill) {
      this.skills= this.skills.filter((value, index, array)=>{
        return value !== skill
      })
    },

    handleSubmit(){
      //Validate password
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long'

      //console everything
      if(!this.passwordError) {
        console.log(this.email)
        console.log(this.password)
        console.log(this.role)
        console.log(this.skills)
        console.log(this.term)
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

  .form .pill {
    display: inline-block;
    background-color: #eee;
    padding: 6px 10px;
    border-radius: 20px;
    margin: 20px 10px 0 0;
    font-weight: bold;
    color: #777;
    letter-spacing: 1px;
    cursor: pointer;
    font-size: 12px;
  }

  .form .submit {
    text-align: center;
  }

  .form .submit button {
    background-color: #0b6dff;
    padding: 10px 20px;
    border:none;
    border-radius: 20px;
    color: white;
    letter-spacing: 1px;
  }

  .form .passwordError p {
    color: #ff0062;
    font-size: 0.8em;
    font-weight: bold;
    letter-spacing: 1px;
    margin: 10px 0 0 0;
  }
</style>