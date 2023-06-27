<script setup>
import { ref, h, markRaw } from 'vue'
import BestSellersSubTab from './components/BestSellersSubTab.vue';
import IWishSubTab from './components/IWishSubTab.vue';

const tabs = [
  {
    title: 'Produits',
    subTabs: [
      {
        title: 'Nos best sellers',
        component: markRaw(BestSellersSubTab)
      },
      {
        title: 'Je souhaite',
        component: markRaw(IWishSubTab)
      },
    ]
  },
  {
    title: 'A propos',
    subTabs: [
      {
        title: 'Produits',
        description: 'Notre vision, nos engagements',
        component: h('img', { src: 'https://www.infomaniak.com/g/static/14ab5bceed3ddb7a31b96574f2f0f3f7/18c14/boris.png' })
      },
      {
        title: 'L\'équipe',
        description: 'Infomakiak, c\'est avant tout une équipe de humaine',
        component: h('img', { src: 'https://www.infomaniak.com/g/static/8ed044808fc14456dc391cae53d88dba/966ce/team.jpg' })
      },
      {
        title: 'Engagement écologique',
        description: 'Nous polluons et nous agissons pour atténuer notre impact',
        component: h('img', { src: 'https://www.infomaniak.com/g/static/6c33ec2e0bcd6ac61d2c117bf37c7b48/bb2e5/environment.png' })
      },
      {
        title: 'Infomaniak recrute',
        description: 'Envie de contribuer à un monde Web plus éthique ?',
        component: h('img', { src: 'https://www.infomaniak.com/g/static/8aae06e79ef278a9c38cb320fdbf72f8/bb2e5/hire.png' })
      },
    ]
  },
  {
    title: 'Support',
    center: true,
    subTabs: [
      {
        title: 'Questions fréquentes',
        description: 'Notre vision, nos engagements'
      },
      {
        title: 'Documentation pour les développeurs',
        description: 'Notre vision, nos engagements'
      },
      {
        title: 'Produits',
        description: 'Notre vision, nos engagements'
      }
    ]
  }
]


const xPosition = ref(0)

const hoveredTab = ref(null)
const hoveredSubTab = ref(null)

const handleMouseOverTab = (event, tab) => {
  hoveredTab.value = tab
  hoveredSubTab.value = tab.subTabs[0]

  const { target } = event
  const { offsetLeft, clientWidth } = target
  xPosition.value = `${offsetLeft + clientWidth / 2}px`
}

const handleMouseOverSubTab = (subTab) => {
  hoveredSubTab.value = subTab
}

const handleMouseLeaveTab = () => {
  hoveredTab.value = null
  hoveredSubTab.value = null
}
</script>

<template>
  <div class="bg-white px-5  flex justify-center" :style="`--x: ${xPosition}`">
    <div class="relative gap-8 flex max-w-[1254px] w-full">
      <img class="my-auto" src="https://www.infomaniak.com/g/static/bfd204f2c114deee99212a7d55778f0d/logo-infomaniak.svg">
      <div class="flex w-full" :class="{ 'relative': hoveredTab?.center }">
        <ul class="flex gap-4 relative" :class="{ 'hover-effect': hoveredTab }">
          <li @mouseover="handleMouseOverTab($event, tab)" v-for="tab in tabs"
            class="px-4 py-8 text-[#000000DE] cursor-pointer hovered">{{
              tab.title }}</li>
        </ul>

        <div @mouseleave="handleMouseLeaveTab"
          class="absolute  bg-[linear-gradient(rgb(45,106,224)_0%,rgb(29,80,213)_100%)] top-full flex"
          :class="hoveredTab.center ? 'translate-x-[calc(var(--x)-50%)]' : 'w-full left-0'" v-if="hoveredTab">
          <ul class="flex-shrink-0 min-w-[300px] flex flex-col p-6">
            <li @mouseover="handleMouseOverSubTab(subTab)"
              class="p-4 rounded-xl hover:bg-white/[.08] cursor-pointer flex flex-col gap-2.5"
              v-for="subTab in hoveredTab.subTabs" :key="subTab">
              <span class="text-white font-bold">{{ subTab.title }}</span>
              <span v-if="subTab.description" class="text-[#D8E3F9]">{{ subTab.description }}</span>
            </li>
          </ul>
          <div class="flex-grow" v-if="hoveredSubTab?.component">
            <component class="w-full h-full" :is="hoveredSubTab.component" />
          </div>

        </div>
      </div>
      <button class="ml-auto bg-[#0098FF] px-3 h-full text-white font-bold">
        Connexion
      </button>
    </div>
  </div>
</template>

<style scoped>
.hover-effect:before {
  content: '';
  position: absolute;
  height: 3px;
  width: 65px;
  bottom: 0;
  transform: translateX(calc(var(--x) - 50%));
  transition: transform 0.3s ease-in-out;
  background-color: #0098FF;
  z-index: 9999;
}
</style>
