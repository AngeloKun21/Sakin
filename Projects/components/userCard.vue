<template>
  <div class="bg-gradient-to-r from-gray-600 to-blue-400">
    <a-col :span="24">
      <a-flex class="pr-28 justify-end items-center">
        <p class="font-mono text-lg text-black">SEARCH</p>
        <input type="text" name="" id="" class="p-1 m-5 bg-transparent border border-solid border-black rounded " v-model="searchValue">
        <a-button type="button" ghost @click="searchButton" class="bg-black text-white">
          <a-flex>
            <SearchOutlined />
          </a-flex>
        </a-button>
      </a-flex>
    </a-col>

    <h1 class="text-black">
      <a-row :gutter="{md: 24, lg:24}" justify="center">
        <a-col :md="20" :sm="24">
          <a-row :gutter="{md:10, lg:20}">
            <a-col class="gutter-row mb-4" :md="4" :sm="10" v-for="(data, index) in fullName" :key="index">
              <div class="gutter-box border rounded-lg border-black">
                <a-card hoverable @click="applicantModal(data)" class="items-center shadow-outline" style="background-color: #AECBEB;"> 
                  <template #cover>
                    <img style="background-color: #E1ECF7;" alt="example" :src="data.image"/>
                  </template>
                  <p class="text-center text-black font-mono font-bold" >{{ data.firstName }} {{ data.lastName }}</p>
                  <a-modal v-model:open="open" @ok="handleOk">
                    <p class="font-mono text-center text-2xl">Name: {{ selectedValue.firstName }} {{ selectedValue.lastName }}</p>
                    <p class="font-mono text-center text-2xl">Age: {{ selectedValue.age }}</p>
                    <p class="font-mono text-center text-2xl">Gender: {{ selectedValue.gender }}</p>
                    <p class="font-mono text-center text-2xl">Email: {{ selectedValue.email }}</p>
                    <p class="font-mono text-center text-2xl">Phone#: {{ selectedValue.phone}}</p>
                    <p class="font-mono text-center text-2xl">BirthDate: {{ selectedValue.birthDate }}</p>
                  </a-modal>
                </a-card>
              </div>
            </a-col>
          </a-row>
        </a-col>
      </a-row>
    </h1>
  </div>
</template>

<script lang='ts' setup>
import { ref, watch } from 'vue'
declare function definePageMeta(meta: any): void;

definePageMeta({
  layout: 'default'
})

interface Data {
  firstName: string,
  lastName: string,
  image: string,
  age: number,
  gender: string,
  email: string,
  phone: string,
  birthDate: string
}
let fullName = ref<Data[]>([]);

async function name() {
  const data = await fetch('https://dummyjson.com/users')
    .then(res => res.json())
    .then(data => { return data.users });

  fullName.value = data
}
name()
//
const searchValue = ref('')
const searchButton = async () => {
  const data = await fetch('https://dummyjson.com/users/search?q=' + searchValue.value)
    .then(res => res.json())
    .then(data => { return data.users });
  fullName.value = data
}
//applicant modal
const open = ref<boolean>(false);

const selectedValue: any = ref();
const applicantModal = (data: object) => {
  open.value = true;
  selectedValue.value = data;
};
const handleOk = (e: MouseEvent) => {
  console.log(e);
  open.value = false;
};

// Auto Search 
watch(searchValue, (newValue) => {
  if (newValue === '') {
    name();
  } else {
    searchButton();
  }
});
</script>