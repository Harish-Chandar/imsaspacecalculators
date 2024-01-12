<script>
    //@ts-nocheck
    let havetakenfinalstext = "I have taken my final...";
    let nottakenfinalstext = "I haven't taken my final...";

    let finalweight = 0;
    let courseweight = 0;
    $: courseweight = 1-finalweight;
    let finalgradeestimate = 0;
    let coursecurrentgrade = 0;
    let coursegradeestimate;
    $: coursegradeestimate = finalgradeestimate*finalweight + coursecurrentgrade*courseweight;

    let gradetoachieve = 0;
    let finalgradecalced = 0;
    $: finalgradecalced = (1/finalweight)*(gradetoachieve - coursecurrentgrade*courseweight);
    $: if (!isFinite(finalgradecalced) || isNaN(finalgradecalced)){
        finalgradecalced = 0;
    }
    let takenFinal = null;

</script>

<h1> Finals Grade Calculator </h1>

{#if takenFinal}
<div id="havetakenfinal">
    <p>There is a simple formula for calculating the impact that the final will have on your grade. Before that, though, we need a few bits of information about the course you are taking:
    </p>
    <form novalidate>
        <label>How much is your final weighted? <input bind:value={finalweight} type="number"></label> <br>
        <label>How much do you think you got on your final (as a decimal)? <input bind:value={finalgradeestimate} type="number"></label> <br>
        <label>What is your current grade in the course (as a decimal)? <input bind:value={coursecurrentgrade} type="number"></label> <br>
        <p>Based on what you told me, I estimate your grade will be: </p>
        <input on:click={()=>{takenFinal = null}} class="backbtn" type="button" value={(coursegradeestimate*100).toFixed(2)}%>
    </form>
</div>
{:else if takenFinal == null}
<div id="mainbtns">
    <button id="yesbtn" class="mainbtns" on:click={()=>{takenFinal = true}} on:mouseenter={() => {
        havetakenfinalstext = "... and I want to see how my grade will be affected by it"
    }} on:mouseleave={() => {
        havetakenfinalstext = "I have taken my final..."
    }}> {havetakenfinalstext} </button>
    <button id="notbtn" class="mainbtns" on:click={()=>{takenFinal = false}} on:mouseenter={() => {
        nottakenfinalstext = "... and I want to see what grade I need to score on it"
    }} on:mouseleave={() => {
        nottakenfinalstext = "I haven't taken my final..."
    }}> {nottakenfinalstext} </button>
</div>
{:else if !takenFinal}
<div id="nottakenfinal">
    <p>There is a simple formula for calculating the impact that the final will have on your grade. Before that, though, we need a few bits of information about the course you are taking: 
    </p>
    <form nonvalidate>
        <label>How much is your final weighted? <input bind:value={finalweight} type="number"></label> <br>
        <label>What is your current grade in the course (as a decimal)? <input bind:value={coursecurrentgrade} type="number"></label> <br>
        <label>What grade do you want in the course (as a decimal)? <input bind:value={gradetoachieve} type="number"></label> <br>
        <p>On your final, you need to score: </p>
        <input on:click={()=>{takenFinal = null}} class="backbtn" type="button" value={(finalgradecalced*100).toFixed(2)}%>
    </form>
</div>
{/if}

<style>
    #mainbtns{
        width:100%;
    }
    h1 {
        font-family: 'Inter', 'Arial', Serif;
    }
    p {
        width: 50%;
        font-family: 'Inter', 'Arial', Serif;
    }
    label {
        font-family: 'Inter', 'Arial', Serif;
    }
    .mainbtns {
        width: 200px;
        min-height: 100px;
        align-content:center;
        border-radius: 50px;
        background-color: #2e3348;
        color: white;
        font-family: 'Inter', 'Arial', Serif;
    }
    .backbtn {
        width: 15%;
        height: 45px;
        align-content:center;
        border-radius: 50px;
        background-color: #2e3348;
        color: white;
        font-family: 'Inter', 'Arial', Serif;
    }
</style>