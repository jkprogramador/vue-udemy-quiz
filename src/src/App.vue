<template>
    <div class="ctr">
        <transition name="fade" mode="out-in">
            <quiz-questions
                v-if="questionsAnswered < questions.length"
                :questions="questions"
                :numberOfQuestions="questions.length"
                :questionsAnswered="questionsAnswered"
                @onQuestionAnswered="onQuestionAnswered"
            />
            <quiz-result v-else :result="result" />
        </transition>
        <button
            type="button"
            class="reset-btn"
            v-if="questionsAnswered >= questions.length"
            @click.prevent="reset"
        >
            Reset
        </button>
    </div>
</template>

<script>
import QuizQuestions from "./components/QuizQuestions.vue";
import QuizResult from "./components/QuizResult.vue";

export default {
    name: "App",
    components: {
        QuizQuestions,
        QuizResult,
    },
    methods: {
        onQuestionAnswered(is_correct) {
            if (is_correct) {
                this.correctAnswers++;
            }

            this.questionsAnswered++;

            if (this.questionsAnswered >= this.questions.length) {
                this.result = this.results.find(
                    (result) =>
                        this.correctAnswers >= result.min &&
                        this.correctAnswers <= result.max
                );
            }
        },
        reset() {
            this.questionsAnswered = 0;
            this.correctAnswers = 0;
        },
    },
    data() {
        return {
            questionsAnswered: 0,
            correctAnswers: 0,
            result: {},
            questions: [
                {
                    q: "What is 2 + 2?",
                    answers: [
                        {
                            text: "4",
                            is_correct: true,
                        },
                        {
                            text: "3",
                            is_correct: false,
                        },
                        {
                            text: "Fish",
                            is_correct: false,
                        },
                        {
                            text: "5",
                            is_correct: false,
                        },
                    ],
                },
                {
                    q: 'How many letters are in the word "Banana"?',
                    answers: [
                        {
                            text: "5",
                            is_correct: false,
                        },
                        {
                            text: "7",
                            is_correct: false,
                        },
                        {
                            text: "6",
                            is_correct: true,
                        },
                        {
                            text: "12",
                            is_correct: false,
                        },
                    ],
                },
                {
                    q: "Find the missing letter: C_ke",
                    answers: [
                        {
                            text: "e",
                            is_correct: false,
                        },
                        {
                            text: "a",
                            is_correct: true,
                        },
                        {
                            text: "i",
                            is_correct: false,
                        },
                    ],
                },
            ],
            results: [
                {
                    min: 0,
                    max: 2,
                    title: "Try again!",
                    desc: "Do a little more studying and you may succeed!",
                },
                {
                    min: 3,
                    max: 3,
                    title: "Wow, you're a genius!",
                    desc: "Studying has definitely paid off for you!",
                },
            ],
        };
    },
};
</script>

<style></style>