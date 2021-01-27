<template>
  <div class="container">
    <div class="form-group mr-5">
      <label>Başlık</label>
      <input v-model="bookmark.title" type="text" class="form-control" />
    </div>
    <div class="form-group mr-5">
      <label>Açıklama</label>
      <input v-model="bookmark.description" type="text" class="form-control" />
    </div>
    <div class="form-group mr-5">
      <label>URL</label>
      <input v-model="bookmark.url" type="text" class="form-control" />
    </div>
    <button v-if="!updateStatus" @click="toSaveData" class="btn-primary mt-10">
      Ekle
    </button>
    <button v-if="updateStatus" @click="$emit('update-data')" class="btn-warning mt-10 mr-5">
      Değiştir
    </button>
    <button v-if="updateStatus" @click="$emit('cancel-update')" class="btn-default mt-10">
      İptal
    </button>
  </div>
</template>
<script>
export default {
  props:["bookmark","updateStatus"],
  methods:{
    toSaveData(){
      this.$emit("save-data",this.bookmark);
    }
  }
}
</script>