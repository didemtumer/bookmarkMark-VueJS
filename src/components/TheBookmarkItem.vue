<template>
  <div class="bookmark-item">
    <div class="header">
      <h3 v-if="!showInputArea">{{ bookmarkItem.title }}</h3>
      <input v-if="showInputArea" v-model="bookmark.title" type="text" class="form-control" />
      <button @click="$emit('delete-data',bookmarkItem.id)" class="btn-sm btn-danger">
        Kaydı Sil
      </button>
    </div>
    <p v-if="!showInputArea" class="mt-20 mb-20">{{ bookmarkItem.description }}</p>
    <input v-if="showInputArea" v-model="bookmark.description" type="text" class="form-control" />
    <div class="d-flex justify-content-between align-items-center">
      <a href="#" v-if="!showInputArea"> {{ bookmarkItem.url }} </a>
      <input v-if="showInputArea" v-model="bookmark.url" type="text" class="form-control" />
      <button @click="$emit('update-item',bookmarkItem)" class="btn-warning btn-sm">
        Düzenle
      </button>
    </div>
  </div>
</template>
<script>
export default {
  props:["bookmarkList","bookmark","bookmarkItem"],
  emits:['delete-data'],
  data(){
    return{
      showInputArea:false
    }
  }

}
</script>