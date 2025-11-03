<script setup>
import { ref, reactive, computed } from "vue";

const msg = ref('Hello!');

const handleClick = () => {
  msg.value = 'world!';
}

const user = reactive({
  name: '홍길동',
  age: '30',
  email: 'gdh@gmail.com'
})

/* v-model, bind */

const title = ref('뷰 바인드 예제');
const imgUrl = ref("https://i.pravatar.cc/300");
const altText = ref('샘플 이미지 사진');
const link = ref("https://vuejs.org");

const imgAttrs = reactive({
  src: "https://i.pravatar.cc/300",
  alt: '샘플 이미지 사진',
  width: '200'
})

const age = ref(0);


function setAge(event){
  age.value = event.target.value;
  console.log(age.value)
}

const enteredGoalValue = ref('');

const goals = reactive([]);

function setGoal(event){
  enteredGoalValue.value = event.target.value;
  console.log(enteredGoalValue);
}

function addGoal(){
  goals.push(enteredGoalValue.value);
  console.log(goals);
}

// computed

const cart = reactive([
  {name: '사과', price: 1300, qty: 3},
  {name: '배', price: 2000, qty:1}
])

const subtotal = computed(()=>
  cart.reduce((sum, item)=> sum + item.price * item.qty, 0)
)

const tax = computed(()=>Math.floor(subtotal.value * .1));

const total = computed(()=>subtotal.value + tax.value);

const formattedTotal = computed(()=>total.value.toLocaleString("ko-KR", {style: "currency", currency: "KRW"}))

const textColor = ref("blue");
const fontSize = ref(20);
console.log(textColor, fontSize);
// 배열 형식 + computed 바인딩
const baseStyle = computed(() => ({
color: 'blue',
fontSize: fontSize.value + "px",
}));
// 배열 형식 + computed 바인딩
const baseStyle2 = computed(() => ({
color: 'red',
fontSize: fontSize.value + "px",
}));

const boxASelected = ref(false);
const boxBSelected = ref(false);
const boxCSelected = ref(false);
console.log(boxASelected, boxBSelected, boxCSelected);
function boxSelected(box) {
if (box === "A") {
boxASelected.value = !boxASelected.value;
} else if (box === "B") {
boxBSelected.value = !boxBSelected.value;
} else if (box === "C") {
boxCSelected.value = !boxCSelected.value;
}
}
</script>
<template>
  <section class="container">
    <h1 @click="handleClick">{{ msg }}</h1>

    <h2>
      user profile
    </h2>
    <p>{{ user.name }}</p>
    <p>{{ user.age }}</p>
    <p>{{ user.email }}</p>

    <h2>v-model bind</h2>
    <h3>{{ title }}</h3>
    <a :href="link"><img :src="imgUrl" :alt="altText"></a>


    <h2>한번에 바인드</h2>
    <a :href="link"><img v-bind="imgAttrs"/></a>

    <h2>조건부 렌더링</h2>
    <input type="number" @input="setAge">
    <li v-if="age<0">입력오류</li>
    <li v-else-if="age<8">미취학</li>
    <li v-else-if="age<18">미성년</li>
    <li v-else>성년</li>

    <div>
      <h2>반복문 렌더링</h2>
      <input type="text" @input="setGoal">
      <button @click="addGoal"></button>
      <p v-if="goals.length === 0">목표를 추가하세요</p>
      <ul v-else></ul>
      <li v-for="goal in goals" :key="goal">{{ goal }}</li>
    </div>

    <div>
      <h2>v-model</h2>
      <input type="text" v-model.trim="enteredGoalValueSec">
      <button @click="addGoal"></button>
      <p v-if="goals.length === 0">목표를 추가하세요</p>
      <ul v-else></ul>
      <li v-for="goal in goals" :key="goal">{{ goal }}</li>
    </div>

    <div>
      <h2>coumptued</h2>
      <ul>
        <li v-for="(item, index) in cart" :key="idex">
          {{ item.name }}: {{ item.price }}원 {{ item.qty }}개
        </li>
      </ul>

      <p>합계: {{ subtotal.toLocaleString() }}</p>
      <p>부가세: {{ tax.toLocaleString() }}</p>
      <p>총합계: {{ formattedTotal }}</p>
    </div>
    
  </section>

  <section id="user-goals">
    <h2>스타일</h2>
    <select v-model="textColor">
    <option value="blue" selected>파랑</option>
    <option value="red">빨강</option>
    </select>
    <select v-model="fontSize">
    <option value="16">16px</option>
    <option value="20" selected>20px</option>
    </select>
    <p :style="{ color: textColor, fontSize: fontSize + 'px' }">
    안녕하세요! 글자 색상과 크기를 바꿔보세요.
    </p>
    <p :style="[baseStyle, baseStyle2]">
    안녕하세요! 글자 색상과 크기를 바꿔보세요.
    </p>
  </section>

  <section id="styling">
    <!-- boxASelected 가 true면 active 클래스가 적용됨 -->
    <div class="demo" :class="{ active: boxASelected }"
    @click="boxSelected('A')">A</div>
    <div class="demo" :class="{ active: boxBSelected }"
    @click="boxSelected('B')">B</div>
    <div class="demo" :class="{ active: boxCSelected }"
    @click="boxSelected('C')">C</div>
  </section>
</template>

<style scoped>
.active {
  border-color: purple; background-color: purple;
}
</style>