<script>

  export default {
    name: 'CatsTab',
    props:{
      cats: {
        type: Array,
        required: true      }
    },

    methods: {
      handleEdit(index , row){
        console.log(index, row)
      },
      handleDelete(index, row){
        console.log(index, row)
      }
    }
  }


</script>

<template>
        <li>{{ cats.length }}</li>

  <el-table :data="cats" style="width: 100%">
      <el-table-column label="Nom" prop="Nom" />
      <el-table-column label="Sexe" prop="Sexe" />
      <el-table-column label="Né le " prop="Né le" />
      <el-table-column label="Prix" prop="Prix" />
      <el-table-column label="Commentaire" prop="Commentaire" />
      <li>{{ cats }}</li>

      <el-table-column align="right">
        <template #default="scope">
          <el-button size="small" @click="handleEdit(scope.$index, scope.row)"
            >Edit</el-button
          >
          <el-button
            size="small"
            type="danger"
            @click="handleDelete(scope.$index, scope.row)"
            >Delete</el-button
          >
        </template>
      </el-table-column>
    </el-table>
</template>

<style scoped>
</style>
