<template>
  <form @submit.prevent="handleSubmit">
    <h1>Vue Form</h1>
    <label>Email:</label>
    <input type="email" v-model="email" />

    <label>Password:</label>
    <input type="password" v-model="password" />
    <span v-if="passwordError">{{ passwordError }}</span>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <div class="terms">
      <input type="checkbox" v-model="terms" required />
      <label>Accept terms and conditions</label>
    </div>

    <label>Skills :</label>
    <input type="text" v-model="temporarySkill" @keyup.space="addSkill" />
    <span v-if="errorMessage">{{ errorMessage }}</span>

    <p
      v-for="(skill, index) in skills"
      :key="index"
      @click="removeSkill(index)"
      class="skill"
    >
      {{ skill }}
    </p>

    <button>Create an Account</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: 'developer',
      terms: false,
      names: [],
      temporarySkill: '',
      skills: [],
      errorMessage: null,
      passwordError: '',
    };
  },
  methods: {
    addSkill() {
      if (!this.skills.includes(this.temporarySkill)) {
        this.skills.push(this.temporarySkill);
        this.errorMessage = null;
      } else {
        this.errorMessage = '❌ This skill has already been added...';
      }
      this.temporarySkill = '';
    },
    removeSkill(index) {
      this.skills.splice(index, 1);
    },
    handleSubmit() {
      //validate password
      this.passwordError =
        this.password.length > 5
          ? ''
          : '❌ Password must be at least 6 chars long';
    },
  },
};
</script>

<style scoped>
form {
  max-width: 420px;
  margin: 5px auto;
  background: #393e46;
  text-align: left;
  padding: 20px;
  border-radius: 10px;
}

h1 {
  text-align: center;
  font-size: 2rem;
}

label {
  color: #ffd369;
  display: inline-block;
  margin: 20px 0 15px;
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  text-transform: uppercase;
}

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  background: #f1f1f1;
  border-bottom: 1px solid #ffd369;
  color: #393e46;
  outline: none;
  font-weight: bold;
}

input[type='checkbox'] {
  display: inline-block;
  width: 20px;
  margin: 0;
  position: relative;
  right: 5px;
}

span {
  display: block;
  margin-top: 5px;
  color: #ff4b5c;
  font-weight: bold;
}

p {
  font-size: 1.1rem;
  text-align: center;
}

.skill {
  display: inline-block;
  margin: 15px 10px 0 0;
  padding: 6px 12px;
  background: #ffd369;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: bold;
  color: #393e46;
  cursor: pointer;
}

button {
  display: block;
  margin: 20px auto 0;
  background: #ffd369;
  border: 1px solid #ffd369;
  padding: 15px 20px;
  color: #393e46;
  font-weight: bold;
  border-radius: 10px;
  cursor: pointer;
  transition: 0.2s;
}

button:hover {
  background: #393e46;
  color: #ffd369;
  border: 1px solid #ffd369;
}
</style>
