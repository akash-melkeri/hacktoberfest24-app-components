<template>
  <q-page class="">
    <component :is="component" v-for="component in components" :key="component"></component>
  </q-page>
</template>

<script>
import { defineComponent, ref, shallowRef } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  setup() {
    return {
      components: ref([])
    }
  },
  methods:{
    importComponents() {
      const components = {}
      const importAll = (r) => {
        Object.keys(r).forEach((key) => {
          const component = r[key].default
          const componentName = key.split('/').pop().replace('.vue', '')
          components[componentName] = shallowRef(component)

        })
      }
      let files = import.meta.globEager('../components/**/*.vue')
      console.log(files, 123)
      importAll(files)
      this.components = components
      return components
    },
  },
  created() {
    this.importComponents()
  }
});
</script>
