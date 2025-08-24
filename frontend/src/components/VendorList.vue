<template>
  <div class="vendor-list">
    <h2>Vendor List</h2>
    <div v-if="vendorStore.loading">Loading vendors...</div>
    <div v-else-if="vendorStore.error" class="error">{{ vendorStore.error }}</div>
    <div v-else-if="vendorStore.vendors.length === 0" class="no-vendors">No vendors found. Add your first vendor!</div>
    <table v-else class="vendors-table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Contact Person</th>
          <th>Email</th>
          <th>Partner Type</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="vendor in vendorStore.vendors" :key="vendor.id">
          <td>{{ vendor.id }}</td>
          <td>{{ vendor.name }}</td>
          <td>{{ vendor.contact_person }}</td>
          <td>{{ vendor.email }}</td>
          <td>{{ vendor.partner_type }}</td>
          <td>
            <button class="icon-btn" @click="openDeleteDialog(vendor.id ?? 0)">
              <font-awesome-icon icon="trash" />
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <div v-if="showDialog" class="dialog-backdrop">
      <div class="dialog">
        <p>Are you sure you want to delete <span class="selected-vendor-name">{{ vendorToDelete?.name }}</span>?</p>
        <div class="dialog-actions">
          <button @click="confirmDelete" class="confirm-btn">Yes</button>
          <button @click="closeDialog" class="cancel-btn">No</button>
        </div>
      </div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useVendorStore } from '../stores/vendorStore';
import type { Vendor } from '../types/Vendor';

// Using the vendor store directly, no need for local props or state
const vendorStore = useVendorStore();

const showDialog = ref(false);
const vendorToDelete = ref<Vendor | null>(null);

onMounted(() => {
  vendorStore.fetchVendors();
});

const openDeleteDialog = (id: number) => {
  vendorToDelete.value = vendorStore.vendors.find(vendor => vendor.id === id) ?? null;
  showDialog.value = true;
};

const closeDialog = () => {
  showDialog.value = false;
  vendorToDelete.value = null;
};

const confirmDelete = () => {
  if (vendorToDelete.value !== null && vendorToDelete.value.id) {
    vendorStore.deleteVendor(vendorToDelete.value.id.toString());
  }
  closeDialog();
};
</script>

<style scoped>
.vendor-list {
  margin: 20px 0;
}

.vendors-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 15px;
}

.vendors-table th,
.vendors-table td {
  padding: 10px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.vendors-table th {
  background-color: #f2f2f2;
  font-weight: bold;
}


.vendors-table tbody tr:nth-child(even) {
  background-color: #f9f9f9;
}

.vendors-table tbody tr:nth-child(odd) {
  background-color: #fff;
}

.vendors-table tbody tr:hover {
  color: #3d74f6
}

.error {
  color: red;
  padding: 10px;
}

.no-vendors {
  padding: 20px;
  text-align: center;
  color: #666;
}

.icon-btn {
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
  color: #f44336;
  font-size: 1.2em;
  display: inline-flex;
  align-items: center;
}

.icon-btn:hover {
  color: #c62828;
}

.dialog-backdrop {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.dialog {
  background: #fff;
  padding: 24px 32px;
  border-radius: 8px;
  box-shadow: 0 2px 16px rgba(0,0,0,0.2);
  min-width: 280px;
  text-align: center;
}

.dialog-actions {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 16px;
}

.confirm-btn {
  background: #fff;
  color: #f44336;
  border: 1px solid #f44336;
  padding: 8px 18px;
  border-radius: 4px;
  cursor: pointer;
}

.cancel-btn {
  background: #ddd;
  color: #333;
  border: none;
  padding: 8px 18px;
  border-radius: 4px;
  cursor: pointer;
}

.confirm-btn:hover {
  background: #c62828;
  color: #fff
}

.cancel-btn:hover {
  background: #bbb;
}

.selected-vendor-name {
  font-weight: bold;
  color: #3d74f6;
}
</style>