<script>
    //@ts-nocheck
    let classes = 0;
    let classarr = [100];
    let namesarr = ["Class 1"];
    $: classes = classarr.length;
    
    function addAClass(){
        // adds a class to the array of classes
        classarr = [...classarr, 100]
        namesarr = [...namesarr, "Class"]
    }
    $: console.log("Grades: " + classarr)
    
    let gpa = 0.00;
    $: gpa = calcGPA(classarr);
    function calcGPA(arr){
        // sum up the arr, convert from percent grade into grade-point, store in separate array, average array
        let gparr = [];
        for (let i = 0; i < arr.length; i++){
            let grade = arr[i];
            if (grade > 92.0){
                gparr = [...gparr, 4.0]; // A+, A
            } else if (grade >= 89.5){
                gparr = [...gparr, 3.7]; // A-
            } else if (grade >= 87.5){
                gparr = [...gparr, 3.3]; // B+
            } else if (grade >= 82.0){
                gparr = [...gparr, 3.0]; // B
            } else if (grade >= 79.5){
                gparr = [...gparr, 2.7]; // B-
            } else if (grade >= 77.5){
                gparr = [...gparr, 2.3]; // C+
            } else if (grade >= 72.0){
                gparr = [...gparr, 2.0]; // C
            } else if (grade > 69.5){
                gparr = [...gparr, 1.7]; // C-
            } else if (grade >= 67.5){
                gparr = [...gparr, 1.3]; // D+
            } else if (grade >= 62.0){
                gparr = [...gparr, 1.0]; // D
            } else if (grade >= 59.5){
                gparr = [...gparr, 0.7]; // D-
            } else {
                gparr = [...gparr, 0]; // F --> Anything lower than a 59.5
            }
        }
        console.log("GPARR: " + gparr);
        let runningtotal = 0.00;
        for (let i = 0; i < gparr.length; i++){
            runningtotal += gparr[i];
        }
        runningtotal = runningtotal/gparr.length;
        return runningtotal;
    }
    function clearclasses(){
        namesarr = [];
        classarr = [];
        classes = 0;
        gpa = 0.00;
    }
</script>

<h1> GPA Calculator </h1>
<p>Every class at IMSA is weighted the same in your GPA and on a 4.0 scale. 
    Keep in mind that colleges recalculate GPA in their own ways. 
    IMSA does not calculate their student's GPA.
</p>
<h2>Does A- mean a GPA of 4.0 or 3.7?</h2>
<p>According to CollegeBoard, PrepScholar, and Collegevine, an A- is a 3.7, while an A and A+ are 4.0.
    In this calculator, an A- is counted as a 3.7.
</p>

<input type="button" value="Add a Class" on:click={addAClass}><br><br>
{#each classarr as aclass, i}
    <label> {i+1}.  Class: <input type="text" bind:value={namesarr[i]}></label>
    <label> Grade: <input type="number" bind:value={classarr[i]}></label><br>
{/each}
<button> GPA: {gpa.toFixed(2)} </button>
<button on:click={clearclasses}> Clear Classes </button>
