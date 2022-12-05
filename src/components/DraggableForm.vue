<template>
  <form>
    <fieldset>
      <legend>Drag and drop is {{ dragAndDropActive ? "on" : "off" }}!</legend>

      <div
        v-for="(inputFieldSet, index) in formData.inputFieldSets"
        :key="index"
        class="input-set"
      >
        <draggable
          :class="[
            'input-flex-container',
            { 'drag-and-drop-active': dragAndDropActive },
          ]"
          ghost-class="ghost-drag-item"
          drag-class="drag-item"
          :group="`editor form ${formData.id}`"
          :disabled="!dragAndDropActive"
          direction="vertical"
          :sort="true"
          :list="inputFieldSet.ids"
          @clone="
            onClone({
              ...$event,
              inputFieldSetIndex: index,
              labelOrField: 'label',
            })
          "
          @change="
            log({
              ...$event,
              group: `editor form ${formData.id}`,
              inputFieldSetIndex: index,
            })
          "
        >
          <!-- add data in list input to tell events apart -->
          <div
            v-for="(id, inputIndex) in inputFieldSet.ids"
            :key="id + 'label'"
            :class="['label' + inputIndex]"
          >
            {{ id }} label
          </div>
        </draggable>
        <draggable
          :class="[
            'input-flex-container',
            { 'drag-and-drop-active': dragAndDropActive },
          ]"
          ghost-class="ghost-drag-item"
          drag-class="drag-item"
          :group="`editor form ${formData.id}`"
          :disabled="!dragAndDropActive"
          direction="vertical"
          :sort="true"
          :list="inputFieldSet.ids"
          @clone="
            onClone({
              ...$event,
              inputFieldSetIndex: index,
              labelOrField: 'field',
            })
          "
          @change="log"
        >
          <div
            v-for="(id, inputIndex) in inputFieldSet.ids"
            :key="id + 'input'"
            :class="['input' + inputIndex]"
          >
            {{ id }} input
          </div>
        </draggable>
      </div>
    </fieldset>
  </form>
</template>

<script>
import draggable from "vuedraggable";
export default {
  name: "DraggableForm",
  components: {
    draggable,
  },
  methods: {
    log: function (evt) {
      window.console.log(evt);
    },
    onClone: function (event) {
      // eslint-disable-next-line no-debugger
      debugger;
      // need: refs to select sister DOM element label/field, to clone for in hand
      window.console.log(event);
    },
  },
  props: {
    dragAndDropActive: Boolean,
    formData: Object,
  },
};
</script>

<style scoped>
* {
  border: 1px solid red;
  margin: 2px;
  padding: 2px;
  display: flex;
}

fieldset {
  flex-wrap: wrap;
  flex-direction: column;
  width: 100%;
}

.input-set {
  flex-wrap: wrap;
  flex-direction: column;
  width: 100%;
}

.input-flex-container {
  flex-wrap: wrap;
  align-items: stretch;
}

.input-flex-container > * {
  flex: 1;
  margin: 0;
}

.label0,
.label1 {
  background-color: aqua;
  align-items: flex-end;
}

.input0,
.input1 {
  background-color: yellow;
}
</style>
