<template>
  <q-layout view="lHh lpR lFf">
    <!-- Top bar -->
    <div class="top-bar">
      <q-btn icon="menu" flat round size="md" class="menu-btn" @click="drawer = !drawer" />
      <q-btn icon="delete" flat round size="md" class="delete-btn" @click="onDelete" />
    </div>

    <q-drawer
      v-model="drawer"
      :width="260"
      bordered
      class="bg-mint sidebar"
      show-if-above
      :breakpoint="420"
    >
      <div class="sidebar-header">
        <div class="sidebar-title"><q-icon name="assignment" /> To-Do List</div>
        <q-btn icon="close" flat round size="md" class="close-btn" @click="drawer = false" />
      </div>
      <q-list>
        <NavLink
          v-for="item in navItems"
          :key="item.id"
          :title="item.title"
          :link="item.link"
          :active="selected === item.id"
          @click="selected = item.id"
        />
      </q-list>
      <q-btn label="Add Item" class="add-btn" @click="onAddItem" />
      <div class="sidebar-bottom-img">
        <img :src="imageUrl" alt="preview" />
      </div>
    </q-drawer>

    <!-- Main Content -->
    <q-page-container>
      <div class="main-content">
        <div class="row q-col-gutter-xl">
          <!-- Title & Date -->
          <div class="col-6">
            <q-item-label>Title</q-item-label>
            <q-input
              filled
              placeholder="new item title"
              dense
              v-model="title"
              style="margin-bottom: 24px"
            />
          </div>
          <div class="col-6">
            <q-item-label>Date</q-item-label>
            <div style="display: flex; align-items: center; gap: 12px">
              <q-input
                v-model="startDate"
                filled
                placeholder="YYYY/MM/DD"
                dense
                style="max-width: 180px"
                mask="####/##/##"
              />
              <span>~</span>
              <q-input
                v-model="endDate"
                filled
                placeholder="YYYY/MM/DD"
                dense
                style="max-width: 180px"
                mask="####/##/##"
              />
            </div>
          </div>
        </div>

        <div class="row q-col-gutter-xl" style="margin-top: 24px; align-items: flex-end">
          <div class="col-6">
            <q-item-label>Image</q-item-label>
            <q-btn
              class="upload-btn"
              style="width: 100%; background: #eaffea; color: #333; margin-bottom: 8px"
              label="Upload Image"
              @click="onUpload"
            />
            <div style="text-align: center; margin-bottom: 8px">or</div>
            <q-input
              filled
              dense
              style="width: 100%"
              placeholder="請輸入圖片網址"
              v-model="imageInput"
            />
          </div>
          <div class="col-6" style="display: flex; flex-direction: column; align-items: center">
            <img
              v-if="imageInput"
              :src="imageInput"
              alt="preview"
              style="width: 100%; border-radius: 16px; object-fit: cover; margin-bottom: 16px"
            />
            <img
              src="https://images.unsplash.com/photo-1562408590-e32931084e23?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
              alt="Chip"
              class="chip-image"
            />
          </div>
        </div>

        <!-- Content -->
        <div class="content-section" style="margin-top: 48px">
          <q-item-label>Content</q-item-label>

          <q-input
            type="textarea"
            filled
            style="
              width: 100%;
              background: #ededed;
              border-radius: 16px;
              min-height: 120px;
              font-size: 1.15rem;
            "
            v-model="content"
            placeholder="content..."
            autogrow
          >
            <template #append>
              <div style="background: #eaffea; border-radius: 0 16px 16px 0; padding: 8px 16px">
                {{ content.length }}/200
              </div>
            </template>
          </q-input>
        </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'
import NavLink from 'src/components/Nav/NavLink.vue'

const drawer = ref(false)

const navItems = [
  { id: 1, title: '1. Item title', link: '#' },
  { id: 2, title: '2. New item title', link: '#' },
]
const selected = ref(2)
const imageUrl = ref(
  'https://images.unsplash.com/photo-1562408590-e32931084e23?q=80&w=1470&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
)

// Main content states
const title = ref('')
const startDate = ref('2022/05/17')
const endDate = ref('2022/05/18')
const imageInput = ref('')
const content = ref('')

function onAddItem() {
  alert('Add Item clicked')
}
function onUpload() {
  alert('Upload Image clicked')
}
</script>

<style scoped>
.bg-mint.sidebar {
  background: #aaffcc;
  display: flex;
  flex-direction: column;
  height: 100vh;
  justify-content: flex-start;
  padding-bottom: 0;
}
.sidebar-header {
  padding: 24px 16px 8px 16px;
}
.sidebar-title {
  font-size: 1.3rem;
  font-weight: bold;
  color: #222;
}
.sidebar-actions {
  padding: 16px;
}

.add-btn,
.q-btn.add-btn,
.q-btn[style*='background: #eaffea'] {
  width: 90%;
  background: #e7ffe9 !important;
  color: #222 !important;
  border-radius: 12px;
  font-weight: 500;
  margin: 12px auto 0 auto;
  box-shadow: none !important;
  display: block;
}

.upload-btn,
.q-btn.upload-btn {
  box-shadow: none !important;
  background: #eaffea !important;
  color: #333 !important;
  border-radius: 12px;
}

.close-btn {
  position: absolute;
  top: 16px;
  right: 16px;
  z-index: 10;
  display: none;
}

.sidebar-bottom-img {
  margin-top: auto;
  padding: 16px;
}
.sidebar-bottom-img img {
  width: 100%;
  height: 60px;
  border-radius: 12px;
  object-fit: cover;
}
.main-content {
  padding: 24px 32px 24px 32px;
}

.row.q-col-gutter-xl {
  margin-top: -24px !important;
  margin-bottom: 12px !important;
}

.main-content {
  position: relative;
}
.top-bar {
  position: relative;
  height: 25px;
}
.delete-btn {
  position: absolute;
  top: 0;
  right: 0;
  z-index: 2;
}

.image-row {
  align-items: center !important;
}

.image-preview-col {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.chip-image {
  display: block;
  margin: 0 auto;
  border-radius: 12px;
  width: 320px;
  height: 120px;
  object-fit: cover;
}

@media (max-width: 420px) {
  .main-content {
    padding: 12px !important;
  }
  .top-bar {
    height: 48px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    position: relative;
  }
  .menu-btn {
    display: inline-flex !important;
    position: absolute;
    left: 8px;
    top: 8px;
    z-index: 10;
  }
  .delete-btn {
    right: 8px;
    top: 8px;
    position: absolute;
    z-index: 10;
  }

  .close-btn {
    display: inline-flex !important;
  }
  .sidebar-header {
    position: relative;
    padding-right: 48px;
  }

  .row.q-col-gutter-xl {
    flex-direction: column !important;
    margin-top: -24px !important;
    margin-bottom: 0 !important;
    gap: 0;
  }
  .col-6 {
    width: 100% !important;
    max-width: 100% !important;
    margin-bottom: -12px;
  }
  .chip-image,
  .image-preview-col img {
    width: 100% !important;
    height: 120px !important;
    border-radius: 12px;
    margin-bottom: 12px;
  }
  .q-input,
  .q-input__control,
  .q-field__control {
    font-size: 1rem !important;
    min-height: 48px !important;
  }
  .content-section {
    margin-top: 24px !important;
  }
  .q-item-label {
    font-size: 1.1rem !important;
    margin-bottom: 4px;
  }
}
</style>
