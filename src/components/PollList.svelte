<script>
    import PollDetails from "./PollDetails.svelte";

    // let poll
    export let currentPolls = [];



</script>

<div class="poll-list">

    <!-- <h4>Current polls:</h4> -->
    {#if currentPolls.length > 0}

        {#each currentPolls as poll (poll.id)}			
            <div>
                <PollDetails {poll}/>
            </div>            
        {/each}

    {/if}
</div>

<style>
    .poll-list{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>