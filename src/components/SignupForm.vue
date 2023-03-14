<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" required v-model="email" />

    <label>Password:</label>
    <input type="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <!-- Role -->
    <label>Role:</label><br />
    <select class="labelcursor" v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <!-- Skills -->
    <label id="skill-label">Skill(s):</label>
    <p class="altcomma">Alt + , to add more</p>
    <input type="text" v-model="tempSkill" @keyup.alt="addSkill" />
    <div v-for="skill in skills" :key="skill" class="pill">
      <span @click="deleteSkill(skill)">{{ skill }}</span>
    </div>

    <br />
    <!-- Celebs -->
    <label id="label-celeb">Select your celeb(s)</label>
    <div class="celeb-ctn">
      <div class="celebs">
        <input id="emmanuel" type="checkbox" value="emmanuel" v-model="names" />
        <label class="labelcursor" for="emmanuel">Emmanuel</label>
      </div>
      <div class="celebs">
        <input id="samuel" type="checkbox" value="samuel" v-model="names" />
        <label class="labelcursor" for="samuel">Samuel</label>
      </div>
      <div class="celebs">
        <input id="gloria" type="checkbox" value="gloria" v-model="names" />
        <label class="labelcursor" for="gloria">Gloria</label>
      </div>
    </div>

    <div class="divider"></div>

    <!-- Terms -->
    <div class="terms">
      <input id="term" type="checkbox" v-model="terms" required />
      <label class="labelcursor" for="term">Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an account</button>
    </div>
  </form>

  <p>Email: {{ email }}</p>
  <p>Password: {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Names: {{ names }}</p>
  <p>Terms accepted: {{ terms }}</p>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "designer",
      terms: false,
      names: [],
      tempSkill: "",
      skills: [],
      passwordError: "",
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill)) {
          this.skills.push(this.tempSkill);
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill) {
      this.skills = this.skills.filter((item) => {
        return skill !== item;
      });
    },
    handleSubmit() {
      // vaidate password
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 chars long";

      if (!this.passwordError) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("role: ", this.role);
        console.log("skills: ", this.skills);
        console.log("celeb: ", this.names);
        console.log("terms accepted: ", this.terms);
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}
label {
  color: #aaa;
  display: inline-block;
  margin: 30px 0 8px;
  font-size: 0.6em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}
#label-celeb{
    margin: 22px 0 0;
}
#skill-label {
  margin-bottom: 5px;
}
.altcomma {
  color: #aaa;
  margin: 0;
  font-size: 0.5em;
  letter-spacing: 0.5px;
  font-weight: bold;
  margin-bottom: 8px;
}
input,
select {
  display: block;
  padding: 6px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
}
.celebs{
    margin-top: 0;
    margin-bottom: 0;

}
.divider {
  display: block;
  padding: 6px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 3px;
  cursor: pointer;
}
.labelcursor {
  cursor: pointer;
}
.pill {
  display: inline-block;
  margin: 8px 8px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}
button {
  background-color: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>
