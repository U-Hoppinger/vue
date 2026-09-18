<script setup>
import { ref, computed } from "vue";
import GlobalClass from "./components/GlobalClass.vue";
import SkillItem from "./components/SkillItem.vue";
// import BaseCard from "./components/BaseCard.vue";
//========================================================
//LET and CONST
//========================================================
const myText = ref("learn");
const newSkillName = ref("");
const activeSkillId = ref(1);

const totalSkills = computed(() => {
  return skills.value.length;
});
const skills = ref([
  { id: 1, name: "ME" },
  { id: 2, name: "SoftSkills" },
  { id: 3, name: "HurdSkills" },
  { id: 4, name: "HTML/CSS" },
  { id: 5, name: "JavaScript" },
  { id: 6, name: "Vue.js" },
  { id: 7, name: "Info" },
]);

const changeText = () => {
  if (myText.value === "learn") {
    myText.value = "New text";
  } else {
    myText.value = "learn";
  }
};
// const toggleIsVisible = () => {
//   isVisible = !isVisible;
// };
// const newSkill = () => {
//   skills.value.push({ id: Date.now(), name: newSkillName.value });
// };
// const removeSkill = (idToRemove) => {
//   skills.value = skills.value.filter((item) => item.id !== idToRemove);
// };
</script>
//========================================================
<template>
  <div class="main-content">
    <div class="left">
      <h2>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Provident dicta
        eveniet iste velit ad quis sed odio, enim culpa? Veniam culpa
        consectetur perferendis sequi exercitationem aliquid soluta dicta
        dolores facilis.
      </h2>
    </div>

    <div class="right">
      <h2>My skills</h2>
      <ul class="menu">
        <SkillItem
          v-for="item in skills"
          :key="item.id"
          :skillName="item.name"
          :class="{ active: activeSkillId === item.id }"
          @choose="activeSkillId = item.id"
        />
        <!--       @click="activeSkillId = item.id" -->
        <!-- <input
        type="text"
        placeholder="Add new skill"
        v-model="newSkillName"
        @keydown.enter="newSkill"
      />
      <button @click="newSkill">Add</button> -->
      </ul>
    </div>
  </div>
</template>
<!-- @delete="removeSkill(item.id)" -->
<!-- @choose="activeSkillId = item.id" -->
<!-- <button @click="changeText">Click me!</button> -->
//========================================================
<style scoped>
/* header {
  line-height: 1.5;
} */

.main-content {
  display: flex;
  flex-direction: row;
  width: 100vw;
  height: 100vh;
  justify-content: center;
  align-items: center;
}
.left,
.right {
  width: 300px;
  height: 300px;
}
.left {
  border-right: 1px solid #42b883;
}
.right {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  margin-left: 10px;
}
.logo {
  display: block;
  margin: 0 auto 2rem;
}

.active {
  color: #42b883;
  font-weight: bold;
  cursor: pointer;
}
ul {
  padding: 0;
  margin: 0;
}
li {
  cursor: pointer;
  padding: 0;
  margin: 0;
}
.menu {
  list-style: none;
}
</style>
