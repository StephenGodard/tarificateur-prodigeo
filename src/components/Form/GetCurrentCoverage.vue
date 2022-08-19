  <template>
<div>
      <!-- Regime Group -->
      <b-form-group label-cols-sm="1" >
        <template v-slot:label>
        Régime <span class="text-danger">*</span>
      </template>

        <b-form-radio-group class="pt-2" id="radio-group-1" v-model="form.regime"
                            name="radio-sub-component">
          <b-form-radio value="General">Général</b-form-radio>
          <b-form-radio value="ALM">Alsace/Moselle</b-form-radio>
        </b-form-radio-group>
      </b-form-group>
      <!-- Required Option Group -->
      <b-form-group label-cols-sm="1" >
        <template v-slot:label>
          Option Actuelle <span class="text-danger">*</span>
        </template>
        <b-form-select v-model="form.currentOption" :options="availableOptions"></b-form-select>
      </b-form-group>
  <!-- Formulas Group-->
  <b-form-group label-cols-sm="1" >  <template v-slot:label>
    Formule Actuelle <span class="text-danger">*</span>
  </template>
    <b-form-select v-model="form.formula" :options="availableFormulas" required></b-form-select>
  </b-form-group>

  <adulte-enfant v-if="form.formula=='Adulte'" v-bind:CurrentCoverage="form"></adulte-enfant>

  <isole-famille v-else-if="form.formula=='Isole'" v-bind:currentCoverage="form"></isole-famille>

  <famille-component v-else-if="form.formula='Familie'" v-bind:currentCoverage="form"></famille-component>


</div>
  </template>

  <script>
  import AdulteEnfant from "@/components/Form/AdulteEnfant";
  import isoleFamille from "@/components/Form/isoleFamille";
  import familleComponent from "@/components/Form/familleComponent";

  export default {
    name: "GetCurrentCoverage",

    data() {
      return {
        form: {
          regime: "",
          currentOption: "",
          formula: "",
        },
        availableOptions: [
          {value: 'Option1', text: "Option 1"},
          {value: 'Option2', text: 'Option 2'}
        ],

        availableFormulas: [
          {value: 'Adulte', text: 'Adulte/Enfant'},
          {value: 'Isole', text: 'Isolé/Famille'},
          {value: 'Familie', text: 'Famille'}
        ],
      }
    },

    components:{AdulteEnfant,isoleFamille,familleComponent}

  }
  </script>
  <style scoped>
  </style>