<script lang="ts">


class TableInfo {
  read: string | undefined = '';
  write: string | undefined = '';
}

const vtables: Map<string, TableInfo> = new Map();

export default {
  data() {
    return {
      tableName: '',
      tables: vtables,
      showBtn: false,
    };
  },
  methods: {
    addReadTable() {
      if (this.tables.has(this.tableName)) {
        const tableInfo = new TableInfo();
        tableInfo.read = 'V';
        tableInfo.write = this.tables.get(this.tableName)?.write;
        this.tables.set(this.tableName, tableInfo);
      } else {
        const tableInfo = new TableInfo();
        tableInfo.read = 'V';
        this.tables.set(this.tableName, tableInfo);
      }
      this.tableName = '';
    },
    delReadTable() {
      if (this.tables.has(this.tableName)) {
        const tableInfo = new TableInfo();
        tableInfo.read = '';
        tableInfo.write = this.tables.get(this.tableName)?.write;
        this.tables.set(this.tableName, tableInfo);
      }
      this.tableName = '';
    },
    addWriteTable() {
      if (this.tables.has(this.tableName)) {
        const tableInfo = new TableInfo();
        tableInfo.read = this.tables.get(this.tableName)?.read;
        tableInfo.write = 'V';
        this.tables.set(this.tableName, tableInfo);
      } else {
        const tableInfo = new TableInfo();
        tableInfo.write = 'V';
        this.tables.set(this.tableName, tableInfo);
      }
      this.tableName = '';
    },
    delWriteTable() {
      if (this.tables.has(this.tableName)) {
        const tableInfo = new TableInfo();
        tableInfo.read = this.tables.get(this.tableName)?.read;
        tableInfo.write = '';
        this.tables.set(this.tableName, tableInfo);
      }
      this.tableName = '';
    },
    delTable() {
      this.tables.delete(this.tableName);
      this.tableName = '';
    },
    showBtnClick() {
      this.showBtn = !this.showBtn;
    }
  },
};

</script>

<template>
  <div class="container">
    <div class="row">
      <form>
        <div class="input-group">
          <span class="input-group-text">
            <img alt="Vue logo" class="logo" src="./../assets/logo.svg" width="20" height="20" /></span>
          <input v-model="tableName" type="text" class="form-control" id="table-name">
          <button type="button" class="btn btn-primary ps-4 pe-4" @click="addReadTable">讀</button>
          <button type="button" class="btn btn-warning ps-4 pe-4" @click="addWriteTable">寫</button>
          <button type="button" class="btn btn-info ps-2 pe-2" @click="showBtnClick">≡</button>
          <button type="button" class="btn btn-danger ps-3 pe-3" v-if="showBtn" @click="delReadTable">×讀</button>
          <button type="button" class="btn btn-danger ps-3 pe-3" v-if="showBtn" @click="delWriteTable">×寫</button>
          <button type="button" class="btn btn-danger ps-3 pe-3" v-if="showBtn" @click="delTable">×刪</button>
        </div>
      </form>
    </div>

    <div class="row">
      <table class="table table-bordered mt-4">
        <thead class="table-light">
          <tr>
            <th>資料表</th>
            <th>讀</th>
            <th>寫</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(table, i) in tables" :key="i">
            <td>{{ table[0] }}</td>
            <td>{{ table[1].read }}</td>
            <td>{{ table[1].write }}</td>
          </tr>
        </tbody>
      </table>
    </div>


  </div>
</template>

<style scoped>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css');
</style>
