<script setup>
import { ref, computed, onMounted } from "vue";
import GlobalClass from "./components/GlobalClass.vue";
import SkillItem from "./components/SkillItem.vue";
// import BaseCard from "./components/BaseCard.vue";
import { skillsData } from "./skillsData.js";
//========================================================
//LET and CONST
//========================================================
const activeSkillId = ref(0);
const skills = ref(skillsData);
const isLoaded = ref(false);
const sandBoxRef = ref(null);

const scrollToSandbox = () => {
  if (sandBoxRef.value) sandBoxRef.value.scrollIntoView({ behavior: "smooth" });
};

onMounted(() => {
  isLoaded.value = true;
});

// вместо резкого появления медленная прогрузка титульной страницы (до прорисовки HTML)

const activeSkillData = computed(() => {
  return skills.value.find((item) => item.id === activeSkillId.value);
}); // возвращает данные при нажатии на какой-то скил справа
</script>
//========================================================
<template>
  <div class="scroll-container">
    <section class="screen">
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
            </ul>
          </div>
        </Transition>
      </div>
      <button class="scroll-btn-down" @click="scrollToSandbox">⬇</button>
    </section>
    <section class="screen sandBox-screen" ref="sandBoxRef">
      <div>
        <div></div>
      </div>
    </section>
  </div>
</template>
//========================================================
<style scoped>
/* контейнер магнит */
.scroll-container {
  height: 100vh;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
  scrollbar-width: none;
}
.scroll-container::-webkit-scrollbar {
  display: none;
}
.screen {
  height: 100vh;
  scroll-snap-align: start;
  position: relative;
}
.scroll-btn-down {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 40px;
  background: transparent;
  border: none;
  color: white;
  cursor: pointer;
}
/* магнит окончен */
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

.descriptionText {
  text-align: center;
}
.menuDescriptionList,
.descriptionText {
  margin-right: 10px;
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

/* вторая вкладка  */
.sandBox-screen {
  padding: 2rem;
}
</style>
