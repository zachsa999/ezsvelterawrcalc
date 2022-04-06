<script>
    import { fade, blur, fly, slide, scale } from 'svelte/transition';
    import { onMount, beforeUpdate, afterUpdate, onDestroy } from 'svelte';
    import Question from "./Question.svelte";
    let score = 0;
    let activeQuestion;
    let quiz;
    let topScore = 1;
    resetQuiz();

    onMount(() => {
        console.log("i mounted");
    });

    beforeUpdate(() => {
        console.log("before Update");
    });

    afterUpdate(() => {
        console.log("after update");
    });

    onDestroy(() => {
        console.log("on destroy");
    });

    function pickAnswer(answer) {
        if (answer == correctAnswer) {
            return (result = "Correct!");
        }
        result = "OOPS!";
    }

    async function getQuiz() {
        const res = await fetch(
            'https://opentdb.com/api.php?amount=10&category=23&difficulty=easy&type=multiple'
            );
        const quiz = await res.json();
        return quiz;
    }

    function nextQuestion() {
        activeQuestion += 1;
    }

    function resetQuiz() {
        activeQuestion = 0;
        quiz = getQuiz();
        score = 0;
    }

    function addToScore() {
        score += 1;
    }

    $: if (score > topScore) {
        score = topScore;
    }
    //reactive declaration
    $: questionNumber = activeQuestion + 1;

</script>

<style>
    .fade-wrapper {
        position: absolute;
    }
</style>

<div>
    <button on:click|once={resetQuiz}>New Quiz</button>
    <h3>My Score : {score}</h3>
    <h4>Question #{questionNumber}</h4>

    {#await quiz}
        Loading....
    {:then data}

        {#each data.results as question, i}
            {#if i == activeQuestion}
            <div in:fly={{ x: 100 }} out:fly={{ x: -200}} class="fade-wrapper">
                <Question {addToScore} {nextQuestion} {question} />
            </div>
            {/if}
        {/each}
    <!-- <button on:click="{handleClick}">Submit</button> -->
    {/await}

</div>




















<!-- 





<script>
    // export 
    let quizName = "Zach Quiz";
    // let title = "";
    let a;
    let b;
    let c;
    
    let operations1 = {
        "+": (a, b) => a + b,
        "-": (a, b) => a - b,
        "*": (a, b) => a * b,
        "/": (a, b) => a / b,
    };

    let operators = [
		{ id: 1, text: `+` },
		{ id: 2, text: `-` },
		{ id: 3, text: `*` },
        { id: 3, text: `/` },
	];
    
    let operator;
    let opSel;
    $: console.log(opSel);

    $: c = operations1["+"](a, b); // c = 6

</script>

 <div>

    <h1>{title}</h1>
    <p>{quizName} is in body</p>
    <input bind:value={title} type="text">
</div> -->

<!-- <div>
    <h1>Calculater</h1>

    <p>Value</p>
    <input bind:value={a} type="number" min="0" max="100000000" />

    <p>Operator(+ - * /)</p>
     <input bind:value={operator} type="text" /> -->
    <!-- <select bind:value={operator} on:change={opSel = operator.text} >
        
        {#each operators as operator }
            <option value={operator}>
                
                {operator.text}
            </option>
            
        {/each}
    </select>

    <p>Operand</p>
    <input bind:value={b} type="number" min="0" max="1000000000" />

    <p>Value</p>
    <p class="huuge">{c}</p>
</div> -->


