<script>
    import { onDestroy, onMount } from 'svelte';
    import PollStore from '../stores/PollStore'
    import PollDetails from "./PollDetails.svelte";

    // let poll
    // export let currentPolls = [];

    // const unsub = PollStore.subscribe((data) => {
    //     currentPolls = data;
    // });

    // onDestroy(() => {
    //     console.log('component destroyed');
    //     unsub();
    // });

</script>

<div class="poll-list">

    <!-- <h4>Current polls:</h4> -->
    {#if $PollStore.length > 0}

        {#each $PollStore as poll (poll.id)}			
            <div>
                <PollDetails {poll} on:vote/>
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