<script setup>
import { log } from 'node_modules/astro/dist/core/logger/core'
import { ref, onMounted } from 'vue'
import cvData from 'src/assets/cv-data.json' 

// New values shold be added at the beginning of the array, same in the cv-data.json file
const tabs = ['EY',  'Card-Dynamics', 'NTT Data' ]

const selectedTab = ref(0)
const selectedComany = ref(cvData[0])

const changeTab = (index) => {
  selectedTab.value = index
  selectedComany.value = cvData[selectedTab.value]
}

const calculateTime = (year, month) => {
  const currentDate = new Date();
  const currentYear = currentDate.getFullYear();
  const currentMonth = currentDate.getMonth() + 1; 

  const monthsDifference = (currentYear - year) * 12 + (currentMonth - month);
  const years = Math.floor(monthsDifference / 12);
  const remainingMonths = monthsDifference % 12;

  const yearText = years > 0 ? `${years} ${years === 1 ? 'year' : 'years'}` : '';
  const monthText = remainingMonths > 0 ? `${remainingMonths} ${remainingMonths === 1 ? 'month' : 'months'}` : '';

  if (years > 0 && remainingMonths > 0) {
    return `${yearText} ${monthText}`;
  } else {
    return yearText || monthText;
  }
}


</script>

<template>
  <!-- TABS SWITCHER -->
  <div class="flex mt-9 ">
      <li v-for="(tab, index) in tabs" v-bind:key="tab" @click="changeTab(index)" 
      class="flex cursor-pointer p-3 px-7 hover:bg-[#1F2937] transition duration-300 ease-in-out border-b-[3px] border-[#353E4B] text-lg" 
      :class="{ 'bg-[#1F2937] border-[#E347C0]' : index===selectedTab  }">
        {{ tab }}
      </li>
  </div>

  <!-- TABS CONTENT -->
  <article  
  class="bg-[#1F2937] w-[100%] mt-2 border-2 border-solid border-[#353E4B] p-5 px-7" >
    <h1 class="text-center ">{{ selectedComany.role }} <span class="text-[#64FFDA]">@ {{ selectedComany.company_name }}</span></h1>
    <h3 v-if="selectedComany.active" class="text-sm text-[#d1d1d1] mt-2">{{ selectedComany.start_month }} {{ selectedComany.start_year }} - Present: {{ calculateTime(selectedComany.start_year, selectedComany.start_month_index) }}</h3>
    <h3 v-if="!selectedComany.active" class="text-sm text-[#d1d1d1] mt-2">{{ selectedComany.start_month }} {{ selectedComany.start_year }} - {{ selectedComany.end_month }} {{ selectedComany.end_year }}: {{ selectedComany.time_worked }}</h3>

    <p  class="mt-5">{{ selectedComany.description }}</p>

    <footer class="mt-7">
      <ul class="flex gap-5">
        <li class="bg-white text-black px-3 rounded-2xl shadow-sm shadow-[#E347C0]" 
        v-for="tag in selectedComany.tags" v-bind:key="tag">
          {{ tag }}
        </li>
      </ul>
    </footer>
  </article>

</template>