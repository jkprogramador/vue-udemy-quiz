<template>
    <div class="result">
        <div class="title">{{ result.title }}</div>
        <div class="desc">{{ result.desc }}</div>
    </div>
</template>

<script>
export default {
    name: "QuizResult",
    props: ["result"],
};
</script>