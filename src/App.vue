<script setup>
import { ref, computed, onMounted } from "vue";
import GlobalClass from "./components/GlobalClass.vue";
import SkillItem from "./components/SkillItem.vue";
// import BaseCard from "./components/BaseCard.vue";
import { skillsData } from "./skillsData.js";
//========================================================
//LET and CONST
//========================================================
const myText = ref("learn");
const activeSkillId = ref(0);
const skills = ref(skillsData);
const isLoaded = ref(false);

onMounted(() => {
  isLoaded.value = true;
});

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
    <Transition name="fade_left">
      <div class="left" v-if="isLoaded">
        <Transition name="switch" mode="out-in">
          <div :key="activeSkillId">
            <p class="descriptionText">
              {{ activeSkillData?.description }}
            </p>
            <ul v-if="activeSkillData?.ability" class="menuDescriptionList">
              <li v-for="point in activeSkillData.ability" :key="point">
                {{ point }}
              </li>
            </ul>
          </div>
        </Transition>
      </div>
    </Transition>
    <Transition name="fade_right">
      <div class="right" v-if="isLoaded">
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
    </Transition>
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
  text-align: center;
}
.menuDescriptionList,
.descriptionText {
  margin-right: 10px;
}

/* .logo {
  display: block;
  margin: 0 auto 2rem;
} */

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
.fade_right-enter-active,
.fade_right-leave-active {
  transition: opacity 2.5s ease;
}
.fade_right-enter-from,
.fade_right-enter-t {
  opacity: 0;
}
.fade_left-enter-active,
.fade_left-leave-active {
  transition: opacity 2.5s ease 1s;
}
.fade_left-enter-from,
.fade_left-enter-t {
  opacity: 0;
}
.switch-enter-active,
.switch-leave-active {
  transition: opacity 0.2s ease;
}
.switch-enter-from,
.switch-leave-to {
  opacity: 0;
}
</style>
