<script>
    export let quizName = "Zach Quiz";
    let title = "";
    let a;
    let b;
    let c;
    let operator;

    
    $: c = eval(a + operator + b); 


</script>

<div>

    <h1>{title}</h1>
    <p>{quizName} is in body</p>
    <input bind:value={title} type="text">
</div>

<div>
    <h1>Calculater</h1>

    <p>Value</p>
    <input bind:value={a} type=number min=0 max=10>

    <p>Operator(+ - * /)</p>
    <input bind:value={operator} type="text">
    
    <p>Operand</p>
    <input bind:value={b} type=number min=0 max=10>

    <p>Value</p>
    <p>{c}</p>

</div>