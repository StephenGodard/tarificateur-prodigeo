<template>

<div>

  <div class="separator"></div>
    <div  v-if="getCover.currentAdultCover != ''">
      <b-form-group v-if="getCoverage.currentOption=='Option1'" >
          <b-form-group  label-cols-sm="1" label="Option envisagée">
               <b-form-select v-if="getCover.coverObl=='yes'" v-model="requestedOption" :options="additionalOption"></b-form-select>

                  <div v-else-if="getCover.coverObl=='no'">



                    <div v-if="getCover.currentChildCover=='noCoverChild'">
                      <div v-if="getCover.currentAdultCover=='noCoverAdult'">
                        <b-form-select v-model="requestedOption" :options="extension"> </b-form-select>
                      </div>

                    </div>


                    <div v-else-if="getCover.currentChildCover=='childExt'">
                      <div v-if="getCover.currentAdultCover=='noCoverAdult'">
                        <b-form-select v-model="requestedOption" :options="extension"></b-form-select>

                      </div>
                    </div>


                    <div v-if="getCover.currentAdultCover=='adultExt'">
                      <div v-if="getCover.currentChildCover=='noCoverChild'">
                        <b-form-select v-model="requestedOption" :options="extension"> </b-form-select>
                      </div>

                      <div v-else-if="getCover.currentChildCover=='childExt'">
                        <b-form-select v-model="requestedOption" :options="additionalOptionCover"> </b-form-select>
                      </div>
                    </div>


                  </div>

            <br/><br/><br/>
            <b-container>

              <b-button variant="primary" @click="onSubmit()">Envoyer</b-button>   <b-button variant="danger" @click="onReset()">Réinitialiser</b-button>
              <br/><br/>


              <b-alert v-if="error=='error'" show variant="danger">Erreur veuillez remplir tout les champs du formulaire</b-alert>
              <keep-alive>
                <b>{{resultValue[1]}}€ par mois</b>
              </keep-alive>
            </b-container>

          </b-form-group>

    </b-form-group>



  <b-form-group v-if="getCoverage.currentOption=='Option2'" label-cols-sm="1" label="Option envisagée">

    <b-form-group   v-if="getCover.currentChildCover=='noCoverChild'">

      <b-form-group v-if="getCover.currentAdultCover=='noCoverAdult'">

      <b-form-select  v-model="requestedOption" :options="additionalOptionCover"></b-form-select>


        <br/><br/><br/>

        <b-container>

          <b-button variant="primary" @click="onSubmit()">Envoyer</b-button>   <b-button variant="danger" @click="onReset()">Réinitialiser</b-button><br/><br/>


          <b-alert v-if="error=='error'" show variant="danger">Erreur veuillez remplir tout les champs du formulaire</b-alert>
          <keep-alive>
            <b>{{resultValue[1]}}€ par mois</b>
          </keep-alive>
        </b-container>

    </b-form-group>
      <div v-else>
      <b-form-select  v-model="requestedOption" :options="additionalOptionCover"></b-form-select>
        <b-container>

          <b-button variant="primary" @click="onSubmit()">Envoyer</b-button>   <b-button variant="danger" @click="onReset()">Réinitialiser</b-button>
          <br/><br/>


          <b-alert v-if="error=='error'" show variant="danger">Erreur veuillez remplir tout les champs du formulaire</b-alert>
          <keep-alive>
            <b>{{resultValue[1]}}€ par mois</b>
          </keep-alive>
        </b-container>
    </div>

  </b-form-group>

    <b-form-group v-else-if="getCover.currentAdultCover=='noCoverAdult'">

      <b-form-select  v-model="requestedOption" :options="additionalOptionCover"></b-form-select>


      <br/><br/><br/>
      <b-container>

        <b-button variant="primary" @click="onSubmit()">Envoyer</b-button>   <b-button variant="danger" @click="onReset()">Réinitialiser</b-button><br/><br/>


        <b-alert v-if="error=='error'" show variant="danger">Erreur veuillez remplir tout les champs du formulaire</b-alert>
        <keep-alive>
          <b>{{resultValue[1]}}€ par mois</b>
        </keep-alive>
      </b-container>


    </b-form-group>

    <b-alert v-else show variant="danger"> Pas d'option supplémentaire disponible </b-alert>



</b-form-group>


</div>
</div>



</template>

<script>

import axios from "axios";

export default {
  name: "quote-validation",

  props:{
    getCoverage:{
      type:Object,
      required:true,
    },
    getCover:{
      type:Object,
      required:true,
    },
    getCoverNumber:{
      type:Object,
      required:true,
    }
  },

  data(){
    return{
      requestedOption:"",
      resultValue:Array,
      error:"",
      additionalOption:[
        {value:"Option2",text:"Option 2"},
      ],
      additionalOptionExt:[
        { value:"Option2Ext",text:"Option 2 "},
      ],
      extension: [
        { value: 'Option1', text: 'Extension Familiale ' },
      ],
      additionalOptionCover:[
        {value:"Option2Ext",text:"Extension Familiale Option 2"}
      ],

      availableNbrChild: [
        {value: 0, text: "0"},
        {value: 1, text: "1"},
        {value: 2, text: "2 et +"},

      ],
    }
  },

  methods:{
    onSubmit(){
      if(this.getCoverage.formula=="Adulte") {
        axios.post('http://localhost:8081/api/execution/invoke',
            {
              "ctx": {
                "properties": [
                  {
                    "key": "quotation.branch",
                    "value": "CoopHLM"
                  },
                  {
                    "key": "quotation.obligatory",
                    "value": "true"
                  },
                  {
                    "key": "quotation.formule",
                    "value": this.getCoverage.formula
                  },
                  {
                    "key": "quotation.year",
                    "value": "2022"
                  },
                  {
                    "key": "quotation.regime",
                    "value": this.getCoverage.regime
                  },
                  {
                    "key": "quotation.requestedOption",
                    "value": this.requestedOption
                  },
                  {
                    "key": "quotation.covers",
                    "complexValues": [
                      [
                        {
                          "key": "code",
                          "value": "Salare"
                        },
                        {
                          "key": "quantity",
                          "value": 1
                        }
                      ],

                      [
                        {
                          "key": "code",
                          "value": "Enfants"
                        },
                        {
                          "key": "quantity",
                          "value": this.getCoverNumber.nbrChild
                        }
                      ],
                      [
                        {
                          "key": "code",
                          "value": "Conjoint"
                        },
                        {
                          "key": "quantity",
                          "value": this.getCoverNumber.nbrAdult
                        }
                      ]
                    ]
                  }
                ]
              },
              "elements": [
                {
                  "code": "ui_calculateCost",
                  "type": "FUNCTION"
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
      }
    },

    onReset(){
      window.location.reload();
    },
  }

}
</script>

<style scoped>
.separator {
  border-bottom: 3px solid #00334D;
  border-radius: 10%;
  margin: auto;
  width: 50%;
  display: block;

  margin-bottom: 5%;
}
</style>