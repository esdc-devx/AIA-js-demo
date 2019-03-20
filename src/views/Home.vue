<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld :survey="Survey" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Model } from "survey-vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

const surveyJSON = {
  title: "Artificial Intelligence Algorithmic Assessment",
  pages: [
    {
      name: "page1",
      questions: [
        {
          type: "radiogroup",
          choices: [
            { text: "Yes (4 pts)", value: 4 },
            { text: "No (0 Pts)", value: 0 }
          ],
          isRequired: true,
          name: "discretion",
          title:
            "Does the recommendation or decision made by the system include elements of discretion?"
        },
        {
          name: "name",
          type: "text",
          requiredIf: "{discretion} contains 'Yes'",
          enabledIf: "{discretion} contains 'Yes'",
          title: "Describe what is discretionary about the decision"
        },
        {
          type: "dropdown",
          name: "car",
          title: "Are the impacts resulting from the decision reversible?",
          isRequired: true,
          colCount: 0,
          choices: [
            { text: "Reversible (1 pt)", value: 1 },
            { text: "Likely Reversible (2 pt)", value: 2 },
            { text: "Difficult to Reverse (3 pt)", value: 3 },
            { text: "Irreversible (4 pt)", value: 4 }
          ]
        }
      ]
    }
  ]
};

@Component({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  readonly Survey: Model = new Model(surveyJSON);
  created() {
    this.Survey.onComplete.add(result => {
      console.log(JSON.stringify(result.data));
    });
  }
}
</script>
