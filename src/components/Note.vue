<template>
  <el-row class="note">
    <div v-if="editMode">
      <div style="margin-bottom: 10px">
        <el-input
          placeholder="Title goes here ..."
          v-model="mynote.title"
          @keydown.native="saveNote"
        ></el-input>
      </div>
      <div style="margin-bottom: 10px">
        <el-select
          @keydown.native="saveTags"
          style="width: 100%"
          v-model="mynote.tags"
          multiple
          filterable
          allow-create
          default-first-option
          placeholder="Enter your tags here..."
        >
          <el-option
            v-for="tag in tags || []"
            :key="tag"
            :label="tag"
            :value="tag"
          >
          </el-option>
        </el-select>
      </div>
      <vue-editor
        v-model="mynote.body"
        class="margin-bottom10"
        style="height: 700px; overflow-y: scroll"
      ></vue-editor>
    </div>
    <div v-else></div>
  </el-row>
</template>
<script>
import { VueEditor } from "vue2-editor";
export default {
  props: ["note", "tags"],
  data() {
    return {
      mynote: {},
      editMode: true,
      saveTimeout: null,
    };
  },
  components: {
    VueEditor,
  },
  watch: {
    note() {
      this.mynote = Object.assign({}, this.note);
    },
  },
  methods: {
    startSaveTimeout() {
      if (this.saveTimeout !== null) return;
      this.saveTimeout = setInterval(() => {
        if (this.mynote.body !== this.note.body) {
          this.saveNote();
        }
      }, 1000);
    },
    clearSaveTimeout() {
      clearInterval(this.saveTimeout);
      this.saveTimeout = null;
    },
    saveNote() {
      this.$emit("savenote", this.mynote);
    },
    saveTags() {
      this.$emit("updatetags", this.mynote.tags);
      this.saveNote();
    },
  },
  mounted() {
    this.startSaveTimeout();
  },
  destroyed() {
    this.clearSaveTimeout();
  },
};
</script>
<style scoped>
.note {
  padding-left: 20px;
}
.quillWrapper {
  overflow: unset !important;
  height: 80vh !important;
}
.ql-container {
  height: 75vh;
}
</style>