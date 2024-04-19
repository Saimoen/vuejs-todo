<template>
    <tr>
      <td>
        <s v-if="item.completed">{{ item.title }}</s>
        <span v-else>{{ item.title }}</span>
      </td>
      <td>
        <input type="checkbox" v-model="item.completed" />
      </td>
    </tr>
  </template>
  


<script>
export default {
    props: {
        item: Object
    },
    mounted() {
    }
}
</script>