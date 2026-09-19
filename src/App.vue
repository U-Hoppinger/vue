<script setup>
import { ref, computed } from "vue";
import GlobalClass from "./components/GlobalClass.vue";
import SkillItem from "./components/SkillItem.vue";
// import BaseCard from "./components/BaseCard.vue";
import { skillsData } from "./skillsData.js";
//========================================================
//LET and CONST
//========================================================
const myText = ref("learn");
const activeSkillId = ref(1);
const skills = ref(skillsData);
const activeSkillData = computed(() => {
  return skills.value.find((item) => item.id === activeSkillId.value);
});

const totalSkills = computed(() => {
  return skills.value.length;
});

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
// const newSkillName = ref("");
</script>
//========================================================
<template>
  <div class="main-content">
    <div class="left">
      <p class="descriptionText">
        {{ activeSkillData?.description }}
      </p>
      <ul v-if="activeSkillData?.ability" class="menuDescriptionList">
        <li v-for="point in activeSkillData.ability" :key="point">
          {{ point }}
        </li>
      </ul>
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

.left {
  border-right: 1px solid #42b883;
  width: 200px;
  height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: flex-end;
}
.right {
  width: 200px;
  height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  margin-left: 10px;
}
.right li {
  width: fit-content;
}

/* .menuDescriptionList {
  display: flex;
  flex-direction: column;
  align-content: center;
} */
.descriptionText {
  text-align: right;
}
.menuDescriptionList,
.descriptionText {
  margin-right: 10px;
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
.menu,
.menuDescriptionList {
  list-style: none;
}
</style>
