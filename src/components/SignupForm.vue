<template>
  <form @submit.prevent="handleSubmit">
    <!-- email -->
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <!-- password -->
    <label>Password:</label>
    <input type="password" required v-model="password" />

    <p v-if="passwordError" class="password-error-msg">
      6 to 12 character and one special character and one number
    </p>

    <!-- skill -->
    <div class="skill-label-wrapper">
      <label>Skill:</label
      ><img
        title="type skill name then press 'alt + ,' to add skill"
        class="alert-img"
        src="../assets/alert.png"
        alt=""
      />
    </div>
    <input type="text" v-model="skill" @keyup.alt="handleAddSkill" />

    <div class="skills-wrapper">
      <p
        @click="handleRemoveSkill(skill)"
        v-for="skill in skills"
        :key="skill"
        class="pill"
      >
        {{ skill }}
      </p>
    </div>

    <!-- role -->
    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <!-- submit -->
    <button type="submit">Sign up</button>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Skills: {{ skills }}</p>
</template>

<script>
export default {
  name: "SignupForm",
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      skill: "",
      skills: [],
      passwordError: false,
    };
  },

  methods: {
    handleAddSkill(e) {
      if (e.key === "," && this.skill && !this.skills.includes(this.skill)) {
        this.skills.push(this.skill);
      }
      this.skill = "";
    },
    handleRemoveSkill(skill) {
      this.skills = this.skills.filter((item) => skill !== item);
    },
    handleSubmit() {
      const regularExpression =
        /^(?=.*[\d])(?=.*[!@#$%^&*])[\w!@#$%^&*]{6,16}$/;

      if (!regularExpression.test(this.password)) {
        this.passwordError = true;
        return;
      }
      this.passwordError = false;
      console.log(this.email, this.password, this.skills, this.role);
      alert("Sign up successful!!");
    },
  },
};
</script>

<style scoped>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.8em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}

select {
  margin-bottom: 10px;
}

button[type="submit"] {
  border: 0;
  padding: 10px 25px;
  background: blue;
  color: white;
  border-radius: 18px;
  cursor: pointer;
  margin-top: 10px;
  text-transform: uppercase;
  font-weight: bold;
}

.skill-label-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
}
.alert-img {
  width: 12px;
  margin-left: 2px;
  margin-top: 10px;
}

.skills-wrapper {
  margin-top: 15px;
}
.pill {
  display: inline;
  background: #d6d6d6;
  padding: 5px 10px;
  border-radius: 15px;
  margin: 5px;
}

.password-error-msg {
  color: red;
  font-size: small;
}
</style>
