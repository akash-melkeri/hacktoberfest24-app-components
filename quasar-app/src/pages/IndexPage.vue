<template>
  <q-page class="">
    <div class="tw-flex tw-justify-between container tw-relative tw-pt-3">
      <div class="tw-absolute tw-bottom-0 tw-bg-gradient-to-r tw-via-white/50 tw-from-white/0 tw-to-white/0 tw-h-0.5 tw-w-full"></div>
      <q-tabs v-model="tab">
        <q-tab name="all" label="All"></q-tab>
        <q-tab name="buttons" label="Buttons"></q-tab>
        <q-tab name="inputs" label="Inputs"></q-tab>
        <q-tab name="others" label="Inputs"></q-tab>
      </q-tabs>
      <div>
        <q-btn-toggle
          v-model="view"
          unelevated
          class="tw-rounded-full tw-bg-white/10"
          no-caps
          toggle-color="primary"
          :options="[
            {slot: 'one', value: 1},
            {slot: 'two', value: 2},
            {slot: 'four', value: 4}
          ]"
        >
          <template v-slot:one>
            <svg xmlns="http://www.w3.org/2000/svg" class="tw-h-6 tw-aspect-square" viewBox="0 0 24 24"><path fill="currentColor" d="M5 17q-.825 0-1.412-.587T3 15V9q0-.825.588-1.412T5 7h14q.825 0 1.413.588T21 9v6q0 .825-.587 1.413T19 17zm0-2h14V9H5zM3.975 5q-.425 0-.7-.288T3 4t.288-.712T4 3h16.025q.425 0 .7.288T21 4t-.288.713T20 5zm0 16q-.425 0-.7-.288T3 20t.288-.712T4 19h16.025q.425 0 .7.288T21 20t-.288.713T20 21zM5 9v6z"/></svg>
          </template>
          <template v-slot:two>
            <svg xmlns="http://www.w3.org/2000/svg" class="tw-h-6 tw-aspect-square" viewBox="0 0 24 24"><path fill="currentColor" d="M8.5 10.5H5q-.825 0-1.412-.587T3 8.5V5q0-.825.588-1.412T5 3h3.5q.825 0 1.413.588T10.5 5v3.5q0 .825-.587 1.413T8.5 10.5M5 8.5h3.5V5H5zM8.5 21H5q-.825 0-1.412-.587T3 19v-3.5q0-.825.588-1.412T5 13.5h3.5q.825 0 1.413.588T10.5 15.5V19q0 .825-.587 1.413T8.5 21M5 19h3.5v-3.5H5zm14-8.5h-3.5q-.825 0-1.412-.587T13.5 8.5V5q0-.825.588-1.412T15.5 3H19q.825 0 1.413.588T21 5v3.5q0 .825-.587 1.413T19 10.5m-3.5-2H19V5h-3.5zM19 21h-3.5q-.825 0-1.412-.587T13.5 19v-3.5q0-.825.588-1.412T15.5 13.5H19q.825 0 1.413.588T21 15.5V19q0 .825-.587 1.413T19 21m-3.5-2H19v-3.5h-3.5zm0-3.5"/></svg>
          </template>
          <template v-slot:four>
            <svg xmlns="http://www.w3.org/2000/svg" class="tw-h-6 tw-aspect-square" viewBox="0 0 24 24"><path fill="currentColor" d="M4 20q-.825 0-1.412-.587T2 18V6q0-.825.588-1.412T4 4h16q.825 0 1.413.588T22 6v12q0 .825-.587 1.413T20 20zm9-2h2.5V6H13zm-4.5 0H11V6H8.5zM4 18h2.5V6H4zm13.5 0H20V6h-2.5z"/></svg>
          </template>
        </q-btn-toggle>
      </div>
    </div>
    <div class="container tw-grid tw-gap-4 tw-mt-4" :class="`${grid_map[view]}`">
      <div class="tw-aspect-video tw-bg-white tw-rounded-lg tw-overflow-hidden" :class="`${container_classes[componentName]}`" v-for="componentName in Object.keys(components_list)" :key="componentName">
        <component :is="components[componentName]" ></component>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, shallowRef } from 'vue';

export default defineComponent({
  name: 'IndexPage',
  setup() {
    return {
      tab: ref('all'),
      view: ref(4),
      components: ref({}),
      grid_map:{
        1: 'tw-grid-cols-1',
        2: 'tw-grid-cols-2',
        4: 'tw-grid-cols-4',
      },
      container_classes: {
        'ButtonOne': 'tw-bg-white tw-flex tw-flex-col tw-items-center tw-justify-center',
      }
    }
  },
  computed: {
    components_list() {
      let out = {}
      Object.keys(this.components).forEach((component) => {
        let file_name = this.components[component].__file.split('quasar-app/src/components/')[1]
        let folder = file_name.split('/')[0]
        if(folder == this.tab || this.tab == 'all') {
          out[component] = this.components[component]
        }
      })
      return out
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
