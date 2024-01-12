<script>
    //@ts-nocheck
    let gpa = 0.00;
    let classes = 0;
    let classarr = [];
    let namesarr = [];
    $: classes = classarr.length;

    function addAClass(){
        classarr = [...classarr, 100]
        namesarr = [...namesarr, "Class"]
    }
    $: console.log(classarr)

    $: calcGPA(classarr)

    function calcGPA(arr){
        // sum up the arr, find out how to calculate GPA
    }
</script>

<h1> GPA Calculator </h1>
<p>Every class at IMSA is graded on a 4 point scales.</p>
<input type="button" value="Add a Class" on:click={addAClass}><br><br>
{#each classarr as aclass, i}
    <label> {i+1}.  Class: <input type="text" bind:value={namesarr[i]}></label>
    <label> Grade: <input type="number" bind:value={classarr[i]}></label><br>
{/each}
<button on:click={calcGPA}> GPA: {gpa} </button>
