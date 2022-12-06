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
          :move="() => false"
          :sort="true"
          :value="inputFieldSet.ids"
          @start="
            log({
              ...$event,
              group: `editor form ${formData.id}`,
              inputFieldSetIndex: index,
            })
          "
          @end="
            log({
              ...$event,
              group: `editor form ${formData.id}`,
              inputFieldSetIndex: index,
            })
          "
        >
          <!-- Wrap label/input in container containing two versions, the regular, and one only displayed when dragging -->
          <div
            v-for="(id, inputIndex) in inputFieldSet.ids"
            :key="id + 'label'"
            class="input-flex-container"
          >
            <div :class="['only-when-not-dragging', 'label' + inputIndex]">
              {{ id }} label
            </div>

            <div class="only-when-dragging">
              <div :class="['label' + inputIndex]">{{ id }} label</div>
              <div :class="['input' + inputIndex]">{{ id }} input</div>
            </div>
          </div>
        </draggable>
        <draggable
          :class="[
            'input-flex-container',
            { 'drag-and-drop-active': dragAndDropActive },
          ]"
          ghost-class="ghost-drag-item"
          drag-class="drag-item"
          :move="() => false"
          :group="`editor form ${formData.id}`"
          :disabled="!dragAndDropActive"
          direction="vertical"
          :sort="true"
          :list="inputFieldSet.ids"
          @start="
            log({
              ...$event,
              group: `editor form ${formData.id}`,
              inputFieldSetIndex: index,
            })
          "
          @end="
            log({
              ...$event,
              group: `editor form ${formData.id}`,
              inputFieldSetIndex: index,
            })
          "
        >
          <div
            v-for="(id, inputIndex) in inputFieldSet.ids"
            :key="id + 'input'"
            :class="['input-flex-container', 'input' + inputIndex]"
          >
            <div :class="['only-when-not-dragging', 'input' + inputIndex]">
              {{ id }} input
            </div>

            <div class="only-when-dragging">
              <div :class="['label' + inputIndex]">{{ id }} label</div>
              <div :class="['input' + inputIndex]">{{ id }} input</div>
            </div>
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

.ghost-drag-item {
  opacity: 0.5;
  /* display: none; */
}

.only-when-dragging {
  display: none;
}

.drag-item .only-when-dragging {
  display: block;
}

.drag-item .only-when-not-dragging {
  display: none;
}
</style>
