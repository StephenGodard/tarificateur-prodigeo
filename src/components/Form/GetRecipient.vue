<template>
  <div>
    <div v-if="currentCoverage.currentChildCover=='noCoverChild'">
      <b-alert show variant="success">Extension familiale Enfant disponible</b-alert>
    </div>

    <div v-if="currentCoverage.currentAdultCover=='noCoverAdult'">
      <b-alert show variant="success">Extension familiale Adulte disponible</b-alert>
    </div>

<div class="separator"></div>


    <!------ ------->


    <b-form-group v-if="currentCoverage.coverObl=='yes'">
      <label><b> Ayant droit Obligatoire :</b></label><br/>
      <label >Nombre d'enfant(s) couvert(s)</label>
      <b-form-select v-model="form.nbrChild" :options="availableNbrChild"></b-form-select>
      <b-form-group>
        <label >Nombre d'adulte(s) couvert(s)</label>
        <b-input-group id="numberChild">
          <b-input-group-prepend>
            <b-btn variant="outline-info" @click="form.nbrAdult--" :disabled="form.nbrAdult<1">-</b-btn>
          </b-input-group-prepend>

          <b-form-input type="number" min="0.00" v-model="form.nbrAdult">{{form.nbrAdult}}</b-form-input>
          <b-input-group-append>
            <b-btn variant="outline-secondary" @click="form.nbrAdult++"  :disabled="form.nbrAdult>4">+</b-btn>
          </b-input-group-append>
        </b-input-group>
      </b-form-group>
    </b-form-group>

    <b-form-group v-else-if="currentCoverage.coverObl=='no'">
      <b-form-group  v-if="currentCoverage.currentChildCover=='childExt'">

        <b-form-group v-if="currentCoverage.currentAdultCover=='adultExt'">
          <b-form-group id="child">
        <label><b> Ayant droit Facultatif :</b></label><br/>
        <label >Nombre d'enfants couvert </label>
        <b-form-select v-model="form.nbrChild" :options="availableNbrChild"></b-form-select>
          </b-form-group>
      <!-------->
      <b-form-group id="Adult">
        <label >Nombre d'adultes couvert</label>
        <b-input-group id="numberChild">
          <b-input-group-prepend>
            <b-btn variant="outline-info" @click="form.nbrAdult--" :disabled="form.nbrAdult<1">-</b-btn>
          </b-input-group-prepend>

          <b-form-input type="number" min="0.00" v-model="form.nbrAdult">{{form.nbrAdult}}</b-form-input>
          <b-input-group-append>
            <b-btn variant="outline-secondary" @click="form.nbrAdult++"  :disabled="form.nbrAdult>4">+</b-btn>
          </b-input-group-append>
        </b-input-group>
      </b-form-group>
      </b-form-group>
      </b-form-group>



      <!--------------------------------------->


      <b-form-group  v-if="currentCoverage.currentChildCover=='noCoverChild'">
        <label><b> Ajout de bénéficiaire :</b></label><br/>
        <label >Nombre d'enfants à couvrir </label>
        <b-form-select v-model="form.nbrChild" :options="availableNbrChild"></b-form-select>
      </b-form-group>
      <!-------->
      <b-form-group v-if="currentCoverage.currentAdultCover=='noCoverAdult'">
        <label><b> Ajout de bénéficiaire :</b></label><br/>
        <label >Nombre d'adultes à couvrir</label>
        <b-input-group id="numberChild">
          <b-input-group-prepend>
            <b-btn variant="outline-info" @click="form.nbrAdult--" :disabled="form.nbrAdult<1">-</b-btn>
          </b-input-group-prepend>

          <b-form-input type="number" min="0.00" v-model="form.nbrAdult">{{form.nbrAdult}}</b-form-input>
          <b-input-group-append>
            <b-btn variant="outline-secondary" @click="form.nbrAdult++"  :disabled="form.nbrAdult>4">+</b-btn>
          </b-input-group-append>
        </b-input-group>
      </b-form-group>

    </b-form-group>


    <quote-validation v-bind:get-cover="currentCoverage" v-bind:get-coverage="getCurrentCover" v-bind:get-cover-number="form"></quote-validation>

  </div>


</template>

<script>


import QuoteValidation from "@/components/Form/QuoteValidation";
export default {
  name: "GetRecipient",
  data() {
    return {
      form: {
        nbrChild: 0,
        nbrAdult: 0,

      },
      availableNbrChild: [
        {value: 0, text: "0"},
        {value: 1, text: "1"},
        {value: 2, text: "2 et +"},

      ],
    }
  },
  props:{
    currentCoverage: {
      type:Object,
      required:true,
    },
    getCurrentCover:{
      type:Object,
      required:true,
    },

  },

  components:{QuoteValidation}

}

</script>

<style scoped>
.separator{
  border-bottom: 3px solid #00334D;
  border-radius: 10%;
  margin: auto;
  width: 50%;
  display: block;
  margin-bottom: 5%;
}
</style>