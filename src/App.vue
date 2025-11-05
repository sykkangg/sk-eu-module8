<script setup>
// import HelloWorld from './components/HelloWorld.vue'
import day1 from './components/day1.vue'
import day2 from './components/day2.vue'
import day22 from './components/day2-2.vue'

import EnrollList from './components/EnrollList.vue'

import {ref, reactive} from 'vue';
const form = reactive({
  name: "",
  email: "",
  phoneNumber: "",
  age: ""
})

const error = reactive({
  name: "",
  email: "",
  phoneNumber: "",
  age: ""
})

const enrolls = ref([]);

let seq = 1;

function validate(field){

  const value = String(form[field] ?? '').trim();

  if(field === 'name'){
    error.name = !value
    ? '이름은 필수 입력입니다'
    : value < 2 || value >22
    ? '이름은 2~22 글자로 입력해주세요'
    : '';
  }

  if(field === 'email'){
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/;

    error.email = !value
    ? '이메일을 입력해주세요'
    : !re.test(value)
    ? "이메일 형식을 확인해주세요"
    : '';
  }

  if(field === 'phoneNumber'){
    const re = /^0\d{1,2}-?\d{3,4}-?\d{4}$/;

    error.phoneNumber = !value
    ? '휴대폰 번호를 입력해주세요'
    : !re.test(value)
    ? "휴대폰 번호 형식을 확인해주세요"
    : '';
  }

  if(field === 'age'){

    const num = Number(value);

    error.age = !value
    ? '나이를 입력해주세요'
    : Number.isNaN(num)
    ? "나이를 숫자로 입력해주세요"
    : num<2 || num > 120
    ? "나이를 확인해주세요"
    : '';
  }

}

function validateAll(){
  Object.keys(form).forEach((f)=>{validate(f);})
  return Object.values(error).every((msg) => !msg)
}

const submitMsg = ref('');

async function onSubmit(){
  submitMsg.value = '';
  if(!validateAll()) {
    submitMsg.value = '입력값을 확인해주세요';
    return;
  } 

  enrolls.value.push({
    id: seq++,
    name: form.name.trim(),
    email: form.email.trim(),
    phoneNumber: form.phoneNumber.trim(),
    age: form.age.trim(),
  })

  console.log(enrolls);

  Object.assign(form, { name: "", email: "", phoneNumber: "", age: "" });

  submitMsg.value = '제출 성공';
}

function removeList(id){
  enrolls.value = enrolls.filter((e)=> e.id != id);
}




</script>

<template>
  <!-- <day1/> -->
  <!-- <day2/> -->
  <!-- <day22/> -->
  <h1>미니 수강 신청 앱 학습</h1>
  <form @submit.prevent="onSubmit">
    <div>
      <label for="name">이름</label>
      <input id="name" type="text" :class="{invalid: error.name}" v-model="form.name" placeholer="홍길동" @blur="validate('name')">
      <small v-if="error.name">{{ error.name }}</small>
    </div>
    <div>
      <label for="email">이메일</label>
      <input id="email" type="text" :class="{invalid: error.email}" v-model="form.email" placeholer="xxx@gmail.com" @blur="validate('email')">
      <small v-if="error.email">{{ error.email }}</small>
    </div>
    <div>
      <label for="phoneNumber">전화번호</label>
      <input id="phoneNumber" type="text" :class="{invalid: error.phoneNumber}" v-model="form.phoneNumber" placeholer="010-0000-0000" @blur="validate('phoneNumber')">
      <small v-if="error.phoneNumber">{{ error.phoneNumber }}</small>
    </div>
    <div>
      <label for="age">나이</label>
      <input id="age" type="text" :class="{invalid: error.age}" v-model="form.age" placeholer="20" @blur="validate('age')">
      <small v-if="error.age">{{ error.age }}</small>
    </div>
    <p v-if="submitMsg" :class="{bad: submitMsg.includes('확인'), ok: submitMsg.includes('성공')}">
      {{ submitMsg }}
    </p>
    <button type="submit">제출하기</button>
    
  </form>

  <h2>신청 목록</h2>
  <EnrollList :items="enrolls" @remove="removeList"/>
</template>

<style scoped>
  form {text-align: left;}
  small {display: block; color: red}
  input.invalid {
    border-color: #ef4444;
    box-shadow: 0 0 0 3px rgba(239, 68, 68, 0.12);
  }
  p.bad {}
</style>
