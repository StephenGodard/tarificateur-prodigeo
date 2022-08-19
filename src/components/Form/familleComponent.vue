<template>

  <div>
    <b-form-group label-cols-sm="1" >
      <template v-slot:label>
        Couverture actuelle <span class="text-danger">*</span>
      </template>
      <b-form-select v-model="owner" :options="ownerFamilie"></b-form-select>
    </b-form-group>



    <div v-if="currentCoverage.currentOption !=''">


  <div class="separator"></div>
  <b-form-group  label-cols-sm="1" >
    <template v-slot:label>
     Option envisagée <span class="text-danger">*</span>
    </template>

    <b-form-group v-if="currentCoverage.currentOption=='Option1'" >

      <b-form-select  v-model="requestedOption" :options="additionalOption"></b-form-select>

      <b-container>
        <br/><br/>
        <b-button variant="primary" @click="onSubmit()">Envoyer</b-button>   <b-button variant="danger" @click="onReset()">Réinitialiser</b-button>
        <br/><br/>

        <b-alert v-if="error=='error'" show variant="danger">Erreur veuillez remplir tout les champs du formulaire</b-alert>
        <keep-alive>
          <b>{{resultValue[1]}}€ par mois</b>
        </keep-alive>
      </b-container>


    </b-form-group>

    <b-alert v-else-if="currentCoverage.currentOption=='Option2'" show variant="danger">Pas d'option supplémentaire disponible</b-alert>

  </b-form-group>
</div>
  </div>
</template>

<script>

import axios from "axios";
export default {
  name: "familleComponent",

  props:{
    currentCoverage:{
      type:Object,
      required:true,
    }
  },

  data(){
    return{
      requestedOption:'',
      additionalOption:[
        {value:'Option2',text:"Option 2"},
      ],
      resultValue:Array,
      error:"",
      owner:"",

      ownerFamilie:[
        {value:'Familie',text:"Famille"}
      ]
    }
  },

  methods:{
    onSubmit(){
      axios.post('http://localhost:8081/api/execution/invoke',
          {
            "ctx": {
              "properties": [
                {
                  "key":"quotation.branch",
                  "value":"CoopHLM"
                },
                {
                  "key":"quotation.obligatory",
                  "value":"true"
                },
                {
                  "key":"quotation.formule",
                  "value":this.currentCoverage.formula
                },
                {
                  "key":"quotation.year",
                  "value":"2022"
                },
                {
                  "key":"quotation.regime",
                  "value": this.currentCoverage.regime
                },
                {
                  "key":"quotation.requestedOption",
                  "value":this.requestedOption
                },


                {
                  "key": "quotation.covers",
                  "complexValues": [
                    [
                      {
                        "key": "code",
                        "value": "Familie"
                      },
                      {
                        "key": "quantity",
                        "value": "1"                  }
                    ],
                  ]
                }


              ]
            },
            "elements": [
              {
                "code":"ui_calculateCost",
                "type":"FUNCTION"
              }
            ]
          }, {

            headers: {
              "Autorization": "Basic YWRtaW46YWRtaW4=",
              "accept": "*/*",
              "Accept": "application/json",
              "Content-Type": "application/json"

            }
          }).then((response) => {
        this.resultValue=response.data.split('b');
        console.log(this.resultValue[1]);
      }).catch((error) => {
        console.log(error)
        console.log(error.response.data);
        this.error="error";
      });
    },

    onReset(){
      window.location.reload()
    }
  }
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