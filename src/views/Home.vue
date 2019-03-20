<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld :survey="Survey"/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import { Model } from "survey-vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

@Component({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  Survey = new Model({
    title: "Tell us, what technologies do you use?",
    pages: [
      {
        name: "page1",
        questions: [
          {
            type: "radiogroup",
            choices: ["Yes", "No"],
            isRequired: true,
            name: "frameworkUsing",
            title: "Do you use any front-end framework like Bootstrap?"
          },
          {
            type: "checkbox",
            choices: ["Bootstrap", "Foundation"],
            hasOther: true,
            isRequired: true,
            name: "framework",
            title: "What front-end framework do you use?",
            visibleIf: "{frameworkUsing} = 'Yes'"
          }
        ]
      },
      {
        name: "page2",
        questions: [
          {
            type: "radiogroup",
            choices: ["Yes", "No"],
            isRequired: true,
            name: "mvvmUsing",
            title: "Do you use any MVVM framework?"
          },
          {
            type: "checkbox",
            choices: ["AngularJS", "KnockoutJS", "React"],
            hasOther: true,
            isRequired: true,
            name: "mvvm",
            title: "What MVVM framework do you use?",
            visibleIf: "{mvvmUsing} = 'Yes'"
          }
        ]
      },
      {
        name: "page3",
        questions: [
          {
            type: "comment",
            name: "about",
            title:
              "Please tell us about your main requirements for Survey library"
          }
        ]
      }
    ]
  });
}
</script>
