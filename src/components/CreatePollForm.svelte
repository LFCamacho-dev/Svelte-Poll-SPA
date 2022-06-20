<script>
    import { createEventDispatcher } from 'svelte';
    let dispatch = createEventDispatcher();

    import Button from '../shared/Button.svelte'

    let fields = { question: '', answerA: '', answerB: ''}
    let errors = { question: '', answerA: '', answerB: ''}
    let valid = false;
    export const newPollEntry = {};

    const submitHandler = () => {
        valid = true;

        //validate question
        if (fields.question.trim().length < 5) {
            valid = false;
            errors.question = 'Question must be at least 5 characters long';
        } else { errors.question = null}
        
        //validate A
        if (fields.answerA.trim().length < 1) {
            valid = false;
            errors.answerA = 'Answer cannot be empty';
        } else { errors.answerA = null}
        
        //validate B
        if (fields.answerB.trim().length < 1) {
            valid = false;
            errors.answerB = 'Answer cannot be empty';
        } else { errors.answerB = null}

        if(valid){

            let poll = {...fields, votesA: 0, votesB: 0, id: Math.random()};
           
           dispatch('AddPollEntry', poll);
        }

    }

</script>

<form on:submit|preventDefault="{submitHandler}">
    <div class="form-field">
        <label for="question">Poll Question</label>
        <input type="text" id="question" bind:value="{fields.question}">
        {#if errors.question != null}
        <div class="error">{errors.question}</div>
        {/if}
    </div>
    
    <div class="form-field">
        <label for="answer-a">Answer A:</label>
        <input type="text" id="answer-a" bind:value="{fields.answerA}">
        {#if errors.answerA != null}
        <div class="error">{errors.answerA}</div>
        {/if}
    </div>
    <div class="form-field">
        <label for="answer-b">Answer B:</label>
        <input type="text" id="answer-b" bind:value="{fields.answerB}">
        {#if errors.answerB != null}
        <div  class="error">{errors.answerB}</div>
        {/if}
    </div>

    <Button type="secondary" flat={true}>Add Poll</Button>          

</form>

<p>{fields.question}</p>
<p>{fields.answerA}</p>
<p>{fields.answerB}</p>

<style>
    form {
        width: 400px;
        margin: 0 auto;
        text-align: center;
    }

    .form-field {
        margin: 18px auto;
    }

    input {
        width: 100%;
        border-radius: 6px;
    }

    label{
        margin: 10px auto;
        text-align: left;
    }

    .error {
        font-weight: bold;
        color: #d91b42;
        font-size: 12px;
    }
</style>