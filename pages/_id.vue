<template>
  <h1 v-if="todo">{{ todo.title }}</h1>
</template>

<script>
import {
  defineComponent,
  useFetch,
  useRoute,
  ref,
  useMeta,
} from '@nuxtjs/composition-api'
export default defineComponent({
  setup() {
    const route = useRoute()
    const { title } = useMeta()
    const { id } = route.value.params
    const todo = ref({})

    useFetch(() =>
      fetch(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then((response) => response.json())
        .then((output) => {
          todo.value = output
          title.value = output.title
        })
    )

    return {
      todo,
    }
  },
  head: {},
})
</script>
