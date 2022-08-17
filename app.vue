<template>
  <div class="text-center mx-72 my-32 w-1/2 h-96">
    <h1 class="text-xl">Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div>
      <div>
        <h4>1) Choose a gender</h4>
        <div>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-3
              border-0
              rounded-2xl
              <!--
              bg-blue-500
              -->
              hover:shadow-blue-500
            "
            :class="options.gender === Gender.BOY && 'bg-orange-200'"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-3
              border-0
              rounded-2xl
              bg-lime-200
              hover:shadow-blue-500
            "
            :class="options.gender === Gender.GIRL && ' bg-pink-400'"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-3
              border-0
              rounded-2xl
              <!--
              bg-gray-300
              -->
              hover:shadow-blue-500
            "
            :class="options.gender === Gender.UNISEX && 'bg-green-700'"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
        </div>
      </div>
      <div>
        <h4>1) Choose the name's papularity</h4>
        <div>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-3
              border-0
              rounded-2xl
              bg-zinc-300
              hover:shadow-blue-500
            "
            :class="options.papuarity === Popularity.TRENDY && 'bg-yellow-500'"
            @click="options.papuarity = Popularity.TRENDY"
          >
            Trendy
          </button>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-3
              border-0
              rounded-2xl
              bg-yellow-200
              hover:shadow-gray-200
            "
            :class="options.papuarity === Popularity.UNIQUE && 'bg-gray-600'"
            @click="options.papuarity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div>
        <h4>1) Choose the name's length</h4>
        <div>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-3
              border-0
              rounded-2xl
              bg-emerald-600
              hover:shadow-blue-500
            "
            :class="options.length === Length.SHORT && ' bg-neutral-200 '"
            @click="options.length = Length.SHORT"
          >
            Short
          </button>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              border-0
              rounded-2xl
              mx-3
              bg-rose-500
              hover:shadow-blue-500
            "
            :class="options.length === Length.LONG && ' bg-sky-400 '"
            @click="options.length = Length.LONG"
          >
            Large
          </button>
          <button
            class="
              h-12
              w-32
              font-large
              px-5
              py-3
              mx-2
              border-0
              rounded-2xl
              bg-emerald-200
              hover:shadow-blue
            "
            :class="options.length === Length.ALL && ' bg-green-400 '"
            @click="options.length = Length.ALL"
          >
            All
          </button>
        </div>
      </div>
      <button
        class="
          h-12
          w-32
          font-large
          px-5
          py-2
          mx-2
          my-8
          border-0
          rounded-2xl
          bg-amber-500
        "
        @click="computedSelectedNames"
      >
        Find Names
      </button>
    </div>
    <div class=" flex mx-48 my-auto">
        <div v-for="name in selectedNames" :key="name">
        <p @click="remove(name)">x</p>
        <h4>{{name}}</h4>
        
        </div>
    </div>
     
  </div>
 
</template>

<script setup lang="ts">
import { reactive } from "vue";
import { Gender, Popularity, Length, names } from "@/data";
interface OptionsState {
  gender: Gender;
  papuarity: Popularity;
  length: Length;
}

const options = reactive<OptionsState>({
  gender: Gender.UNISEX,
  papuarity: Popularity.TRENDY,
  length: Length.LONG,
});

const selectedNames = ref<string[]>([]);

const computedSelectedNames = () => {
  const filterNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.papuarity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });

    selectedNames.value=filterNames.map(name => name.name)
    console.log(filterNames)
};

// const remove =(name)=>{
//   selectedNames.value=selectedNames.value.filter((t)=>t !== name)
// }

const remove=(name) => {
 const index= selectedNames.value.findIndex((n)=> name==n)
 console.log(index)
 selectedNames.value.splice(index,1)
}

</script>
