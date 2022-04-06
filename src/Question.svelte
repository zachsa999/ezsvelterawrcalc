<script>
    export let question;
    export let nextQuestion;
    export let addToScore;

    let isCorrect;
    let isAnswered = false;
    let answers = question.incorrect_answers.map(answer => {
        return {
            answer,
            correct: false
        };
    });
    // let correctAnswers = question.correct_answer;

    
    let allAnswers = [
        ...answers,
        {
            answer: question.correct_answer,
            correct: true
        }
    ];
    
    shuffle(allAnswers);

    function shuffle(array) {
        array.sort(() => Math.random() - 0.5)
    }

    function checkQuestion(correct) {
        if (!isAnswered) {
            isAnswered = true;
            isCorrect = correct;
            if (correct) {
                addToScore();
            }
        }
    }

</script>



<div>
    <h3>{@html question.question}</h3>
    
    {#each allAnswers as answer}
    <button on:click={() => checkQuestion(answer.correct)}>
        {@html answer.answer}
    </button>
    {/each}

    {#if isAnswered}
    <h4>
        {#if isCorrect} 
            You got it right
        {:else}
            You bad frank
        {/if}
    </h4>
    {/if}

    {#if isAnswered}
    <div>
        <button on:click={nextQuestion}>Next Question</button>
    </div>
    {/if}
    <!-- <button>{correctAnswers}</button> -->

</div>