# vue-stopwatch

> Simple implementation project to get familiar with Vue 3

Simple stop-watch web application with Vue 3

In this project, I understood the ref and computed provided by Vue 3's composition api and how the emit used in Vue 2 changed. This repository is just stop-watch web application that has functions of start, stop and reset.

## emit

in Vue 2:

```vue
// parent
<template>
  <child-component @something="parentMethod" />
</template>

<script>
export default {
  methods: {
    parentMethod() {
      console.log('emit from child');
    }
  }
};
</script>

// child
<template>
  <button @click="handleEmit">
    emit
  </button>
</template>

<script>
export default {
  methods: {
    handleEmit() {
      // can give 2th argument to send data to parent
      this.$emit('something', ...)
    }
  }
}
</script>
```

in Vue 3:

```vue
// parent
<template>
  <child-component @something="parentMethod">
</template>

<script>
export default {
  setup() {
    const parentMethod = () => {
      console.log('emit from child');
    }
  }
}
</script>

// child
<template>
  <button @click="$emit('something')">
    emit
  </button>
</template>

<script>
export default {
  emits: ['something']
}
</script>
```

Vue 3 is so cool than Vue 2.
