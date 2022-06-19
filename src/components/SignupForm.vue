<template>
  <form @submit.prevent="handleSubmit">
    <!-- email -->
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <!-- password -->
    <label>Password:</label>
    <input type="password" required v-model="password" />

    <!-- skill -->
    <label>Skill:</label>
    <input type="text" v-model="skill" @keyup.alt="handleAddSkill" />
    <div class="skills-wrapper">
      <p v-for="skill in skills" :key="skill" class="pill">
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
  <p>Skill: {{ skill }}</p>
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
      skills: ["html", "css", "vue"],
    };
  },

  methods: {
    handleAddSkill(e) {
      console.log(e);

      if (e.key === ",") {
        this.skills.push(this.skill);
      }
      this.skill = "";
    },
    handleSubmit() {
      console.log(this.email, this.password);
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
  font-size: 0.6em;
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
</style>
