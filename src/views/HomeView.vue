<template>
  <div class="home">

    <h2>{{ appTitle }}</h2>

    <h3>{{ counterData.title }}:</h3>

    <div>
      <button @click="decreaseCounter(2)" class="btn">--</button>
      <button @click="decreaseCounter(1)" class="btn">-</button>
      <span class="counter">{{ counterData.count }}</span>
      <button @click="increaseCounter(1)" class="btn">+</button>
      <button @click="increaseCounter(2)" class="btn">++</button>
    </div>
    <br>
    <p>This counter is {{ determineExpression }}</p>

    <div class="edit">
      <h4>Edit Counter title</h4>
      <input v-model="counterData.title" type="text" v-autofocus>
    </div>

  </div>
</template>

<script setup>
import { ref, reactive, computed, watch } from 'vue'
import { vAutofocus } from '../directives/vAutofocus';


// const counter = ref(0),
//       counterTitle = ref('My Counter')

// There are times when data properties don't need to be reactive, so we make it non-reactive. Below is the method and then add it normally inside a double curly in the template above.
const appTitle = 'My Dope Counter'

// 
const counterData = reactive({
  count: 0,
  title: 'My Counter'
})

// If we use a ref data property, the watch expression is simply 
// watch(count) if we used the above ref data. We can't do the same thing to a reactive object since it is a nested data property. 
watch(() => counterData.count, (newCount, oldCount) => {
  if (newCount === 20)
    alert('You got it')
})

// computed properties are usually generated based on reactive data, which are cached and updated only when the dependencies change
const determineExpression = computed(() => {
  if (counterData.count % 2 === 0) return 'even'
  return 'odd'
})

const increaseCounter = amount => {
  counterData.count += amount
}

function decreaseCounter(amount) {
  counterData.count -= amount
}

</script>

<!-- Option API way to using data(), computed, watch and hooks

<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  computed: {
    myComputedProperty() {
      return 'my result'
    }
  },
  watch: {
    count(newCount, oldCount) {
      if (newCount == 20) alert('You hit 20')
    }
  },
  mounted() {
    // do stuff when component is loaded
    console.log('mounted')
  },
  unmounted() {
    console.log('unmounted')
  },
  directives: {
    autofocus: {
      mounted(el) {
        el.focus()
      }
    }
  }
}

</script> -->

<!-- Original way of using composition API before script setup was introduced -->
<!-- <script>
import{ ref } from 'vue'

export default {
  setup() {
    const counter = ref(0)
    // 1st method of declaring a function/method
    const increaseCounter = () => {
      // When a ref is created, an object is created, the value of the ref will be stored in a property called 'value'
      counter.value++ 
    }
    // 2nd method of declaring a function/method
    function decreaseCounter() {
      counter.value--
    }
    return{
      counter,
      increaseCounter,
      decreaseCounter
    }
  }
}
</script> -->


<!-- Original options api way of doing things -->
<!-- <script>
export default {
  data() {
    return {
      counter: 0,
    }
  },
  methods: {
    increaseCounter() {
      this.counter++
    },
    decreaseCounter() {
      this.counter --
    }
  }
}
</script> -->

<style>
.home {
  text-align: center;
  padding: 20px;
}

.btn .counter {
  font-size: 40px;
  margin: 200px;
}

.edit {
  margin-top: 60px;
}
</style>