<template>
<div>
  <b-form-group label-cols-sm="1" >
    <template v-slot:label>
      Ayant droit Obligatoire ? <span class="text-danger">*</span>
    </template>
    <b-form-radio-group class="pt" id="radio-group-2" v-model="cover.coverObl"
                        name="radio-component" >
      <b-form-radio value="yes">Oui</b-form-radio>
      <b-form-radio value="no">Non</b-form-radio>
    </b-form-radio-group>
  </b-form-group>
<div v-if="cover.coverObl!=''">
  <b-form-group label-cols-sm="1" label="Couverture Enfants Actuelle">
    <b-form-select v-if="cover.coverObl=='yes'" v-model="cover.currentChildCover" :options="CurrentChildCoverObl"></b-form-select>
    <b-form-select v-else-if="cover.coverObl=='no'" v-model="cover.currentChildCover" :options="CurrentChildCoverOpt"></b-form-select>
    <br/>
  </b-form-group>
  <b-form-group  label-cols-sm="1" label="Couverture Adulte Actuelle">
    <b-form-select v-if="cover.coverObl=='yes'" v-model="cover.currentAdultCover" :options="CurrentAdultCoverObl"></b-form-select>
    <b-form-select v-else-if="cover.coverObl=='no'" v-model="cover.currentAdultCover" :options="CurrentAdultCoverOpt"></b-form-select>
  </b-form-group>

  <get-recipient v-bind:get-current-cover="CurrentCoverage" v-bind:current-coverage="cover"></get-recipient>

</div>










</div>
</template>

<script>

import getRecipient from "@/components/Form/GetRecipient";
export default {
  name: "AdulteEnfant",
  components: {getRecipient},
  data(){
    return{
      cover:{
        coverObl:"",
        currentChildCover:"",
        currentAdultCover:"",

      },
      CurrentChildCoverObl:[
        {value:"childObl",text:"Enfant(s) obligatoire"},
      ],
      CurrentChildCoverOpt:[
        {value:"noCoverChild",text:"Pas de couverture"},
        {value:"childExt",text:"Enfant(s) Facultatif 'extension familiale' "}
      ],
      CurrentAdultCoverObl:[
        {value:"AdultObl",text:"Adulte obligatoire"},
      ],
      CurrentAdultCoverOpt:[
        {value:"noCoverAdult",text:"Pas de couverture"},
        {value:"adultExt",text:"Adulte Facultatif 'extension familiale' "}
          ],
    }
  },
  props: {
    CurrentCoverage: {
      type: Object,
      required: true,
    },


  }
}
</script>

<style scoped>

</style>