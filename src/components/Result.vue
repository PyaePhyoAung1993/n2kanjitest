<template>
  <div class="result">
    <!-- <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div> -->
    <div class="title">
      Your Score is : {{ totalCorrect }} in {{ questions.length }}
    </div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

<script>
export default {
  props: ["results", "totalCorrect", "questions"],
  computed: {
    resultIndex() {
      let index = 0;

      this.results.forEach((e, i) => {
        if (e.min <= this.totalCorrect && e.max >= this.totalCorrect) {
          index = i;
        }
      });
      return index;
    },
  },
};
</script>

