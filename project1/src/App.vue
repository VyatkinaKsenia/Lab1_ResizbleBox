<template>
  <div id="app">
    <h1>Создание изменений размера окна</h1>
    <ResizableBox />
  </div>
</template>

<script>
import ResizableBox from './components/ResizbleBox.vue';

export default {
  name: 'App',
  components: {
    ResizableBox
  }
}
</script>
