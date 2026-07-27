<template>
  <form @submit.prevent="handleSubmit" class="form-card"> 
    <h2 class="form-title">Create Account</h2>

    <label>Email:</label> 
    <input type="email" required v-model="email" placeholder="example@domain.com"> 

    <label>Password:</label> 
    <input type="password" required v-model="password" placeholder="••••••••"> 
    <div v-if="passwordError" class="error">{{ passwordError }}</div>
    
    <label>Role:</label> 
    <select v-model="role">
      <option value="" disabled selected>Select your role</option>
      <option value="developer">Web Developer</option> 
      <option value="designer">Web Designer</option>
    </select> 

    <label>Skills (Press Alt + comma to add):</label>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" placeholder="e.g. Vue.js">
    <div class="skills-container">
      <div v-for="skill in skills" :key="skill" class="pill" @click="deletSkill(skill)"> 
        <span>{{ skill }} &times;</span>
      </div>
    </div>

    <div class="terms">  
      <input type="checkbox" id="terms-check" required v-model="terms"> 
      <label for="terms-check">Accept Terms and Conditions</label>
    </div> 

    <div class="submit">
      <button type="submit">Create an Account</button>
    </div>

    <!-- التوقيع الفخم -->
    <div class="footer-credit">
      ♡ made by <span>little coder janawi</span> ♡
    </div>
  </form> 

  <!-- عرض البيانات المباشر -->
  <div class="preview-box">
    <p><strong>Email:</strong> {{ email }}</p> 
    <p><strong>Role:</strong> {{ role }}</p> 
    <p><strong>Terms:</strong> {{ terms ? 'Accepted' : 'Not Accepted' }}</p>
  </div>
</template>

<script>
export default {
  name: 'SignupForm',
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e) {
      if (e.key === ',' && this.tempSkill.trim()) {
        const cleanSkill = this.tempSkill.replace(',', '').trim()
        if (!this.skills.includes(cleanSkill)) {
          this.skills.push(cleanSkill) 
        }
        this.tempSkill = ''
      }
    },
    deletSkill(skill) {
      this.skills = this.skills.filter((item) => skill !== item) 
    },
    handleSubmit() {
      // Validate password
      this.passwordError = this.password.length > 5 ? 
        '' : 'Password must be at least 6 characters long' 

      if (!this.passwordError) {
        console.log('Form Submitted Successfully!')
        console.log('Email:', this.email)
        console.log('Role:', this.role)
        console.log('Skills:', this.skills)
      }
    }
  }
}
</script>