<script setup>
import _ from 'lodash'
import { computed, reactive, ref } from 'vue'

  const props = defineProps({
    cats: Array
  })
    
  const catsArray = ref(props.cats)
  const dialogFormVisible = ref(false) 
  const title = ref("Add Cat") 
  const formLabelWidth = '140px'

    const form = reactive({
        id:'',
        nom: '',
        sexe: '',
        date: '',
        race: '',
        prix: '',
        commentaires: ''
    })

  const addCat = () => {

     // Si on a un id c'est une modif sinon une création
    if(form.id === ''){
        catsArray.value.push({
        "id" : catsArray.value.length +1, 
        "Nom": _.capitalize(form.nom),
        "Sexe": form.sexe,
        "Date": form.date,
        "Race": _.capitalize(form.race),
        "Prix": form.prix,
        "Commentaires": _.capitalize(form.commentaires)
      })
    } else {

       _.forEach(catsArray.value , c => {
         if(c.id == form.id){
          c.Nom = _.capitalize(form.nom)
          c.Sexe = form.sexe
          c.Date = form.date
          c.Race = _.capitalize(form.race)
          c.Prix = form.prix
          c.Commentaires = _.capitalize(form.commentaires)
         }

       })
    }
    
    handleClose()
  }

  const handleEdit = (row) => {
    title.value  = 'Modifier un chat'
    dialogFormVisible.value = true
    form.id = row.id
    form.nom = row.Nom
    form.sexe = row.Sexe
    form.date = row.Date
    form.race = row.Race
    form.prix = row.Prix
    form.commentaires = row.Commentaires
  }

  const handleDelete = (row) => {
      _.remove(catsArray.value, c => c.id == row.id);
  }

  const handleClose = () => {
    //On reset le formulaire à la fermeture du modal
    dialogFormVisible.value = false
    form.id = ''
    form.nom = ''
    form.sexe = ''
    form.date = ''
    form.race = ''
    form.prix = ''
    form.commentaires = ''
  }

  const search = ref('')
  const filterTableData = computed(() =>
  catsArray.value.filter(
    (data) =>
      !search.value ||
      data.Nom.toLowerCase().includes(search.value.toLowerCase()) ||
      data.Sexe.toLowerCase().includes(search.value.toLowerCase()) ||
      data.Date.toLowerCase().includes(search.value.toLowerCase()) ||
      data.Race.toLowerCase().includes(search.value.toLowerCase()) ||
      (_.toString(data.Prix)).toLowerCase().includes(search.value.toLowerCase()) ||
      data.Commentaires.toLowerCase().includes(search.value.toLowerCase()) 

  )
)

</script>

<template>
  <!--table des chats-->
  <el-table :data="filterTableData" style="width: 100%">
      <el-table-column label="Nom" prop="Nom"  sortable/>
      <el-table-column label="Sexe" prop="Sexe" sortable />
      <el-table-column label="Né le" prop="Date" sortable />
      <el-table-column label="Race" prop="Race" sortable />
      <el-table-column label="Prix" prop="Prix" sortable/>
      <el-table-column label="Commentaires" prop="Commentaires" width=380 sortable/>
      <el-table-column width  = 250>
        <template #header>
        <el-input v-model="search" size="small" placeholder="Saisissez votre recherche" />
      </template>
        <template #default="scope">
          <el-button size="small" type="info" @click="handleEdit(scope.row)"
            >Modfier</el-button
          >
          <el-button
            size="small"
            type="danger"
            @click="handleDelete(scope.row)"
            >Supprimer</el-button
          >
        </template>
      </el-table-column>
  </el-table>
  <el-button class="mt-4" style="width: 100%" type="success" @click="dialogFormVisible = true ; title  = 'Ajouter un chat'"
    >Ajouter un chat</el-button
  >
  <!--Modal création et ajout des chats-->
  <el-dialog v-model="dialogFormVisible" :title="title">
    <el-form :model="form">
      <el-form-item label="Nom" :label-width="formLabelWidth">
        <el-input v-model="form.nom"/>
      </el-form-item>
      <el-form-item label="Sexe" :label-width="formLabelWidth">
        <el-select v-model="form.sexe" placeholder="Sexe">
          <el-option label="Femelle" value="Femelle" />
          <el-option label="Mâle" value="Mâle" />
      </el-select>      
    </el-form-item>
      <el-form-item label="Né le " :label-width="formLabelWidth">
        <el-date-picker
        v-model="form.date"
        type="date"
        placeholder="Pick a day"
        size="small"
        format="YYYY/MM/DD"
        value-format="YYYY-MM-DD"
      />
      </el-form-item>
      <el-form-item label="Race" :label-width="formLabelWidth">
        <el-input v-model="form.race"/>
      </el-form-item>
      <el-form-item label="Prix" :label-width="formLabelWidth">
        <el-input-number v-model="form.prix"/>
      </el-form-item>
      <el-form-item label="Commentaires" :label-width="formLabelWidth">
        <el-input v-model="form.commentaires" type="textarea" />
      </el-form-item>
    </el-form>
    <template #footer>
      <span class="dialog-footer">
        <el-button @click="handleClose()">Annuler</el-button>
        <el-button type="primary" @click="addCat()"
          >Valider</el-button
        >
      </span>
    </template>
  </el-dialog>
</template>

<style scoped>
</style>
