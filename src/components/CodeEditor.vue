<template>
    <div :id="editorId" class="content-box flask-editor">function calcIteration(fuel, speed, height) {
  // For every loop iteration, you will get 3 values:
  // fuel: remaining fuel (0-100)
  // speed: vertical speed
  // height: height of the lander
  // (0 = ground , 4000 = initial position)

  // ::::::::::::::::::
  // Add your code here
  // To win the game, you must land with speed lte 90
  // ::::::::::::::::::

  // Return engine power value (0-4)
  // Note: Only integer values allowed
  return 0;
}</div>
</template>

<script>
import CodeFlask from 'codeflask';
var editorObj;

export default {
    name: 'CodeEditor',
    props: [ 'name', 'bus' ],

    data: function() {
        return {
            editorId: this.name + "-flask"
        };
    },

    methods: {
      fetchCode: function() {
        this.bus.$emit('transmitcode', editorObj.getCode());
      }
    },

    mounted: function() {
        editorObj = new CodeFlask(
            document.getElementById(this.editorId), { language: 'js' }
        );

        this.bus.$on('requestcode', this.fetchCode);
    },

    beforeDestroy: function() {
        this.bus.$off('requestcode');
    }
}
</script>

<style scoped>
    .flask-editor {
        min-height: 600px;
    }
</style>
