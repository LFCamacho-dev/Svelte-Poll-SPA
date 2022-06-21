<script>
    import { createEventDispatcher } from 'svelte';
    let dispatch = createEventDispatcher();

    import Card from '../shared/Card.svelte'
    export let poll;

    $: totalVotes = poll.votesA + poll.votesB

    $: percentageA = Math.floor(100 / totalVotes * poll.votesA);
    $: percentageB = Math.floor(100 / totalVotes * poll.votesB);
    // $: percentageB = totalVotes * 100 / votesB;
    

    const handleVote = (option, id) => {
        dispatch('vote', {option, id});
    };

    
</script>

<Card>
    <div class="poll">
        <h3>{poll.question}</h3>
        <p>Total Votes: {totalVotes}</p>
        <div class="answer" on:click={() => handleVote('a', poll.id)}>
            <div class="percent percent-a" style="width:{percentageA}%"></div>
            <!-- <div on:click="{() => poll.votesA ++}" class="percent percent-a"> -->
            <span>{poll.answerA} ({poll.votesA} votes)</span>
            
        </div>
        <div class="answer" on:click={() => {handleVote('b', poll.id)}}>
            <div class="percent percent-b" style="width:{percentageB}%;"></div>
            <!-- <div on:click="{() => poll.votesB ++}" class="percent percent-b"> -->
            <span>{poll.answerB} ({poll.votesB} votes)</span>
            
        </div>                
    </div>
</Card>

<style>
    h3{
      margin: 0 auto;
      color: #555;
    }
    p{
      margin-top: 6px;
      font-size: 14px;
      color: #aaa;
      margin-bottom: 30px;
    }
    .answer{
      background: #fafafa;
      cursor: pointer;
      margin: 10px auto;
      position: relative;
    }
    .answer:hover{
      opacity: 0.6;
    }
    span{
      display: inline-block;
      padding: 10px 20px;
    }
    .percent{
      height: 100%;
      position: absolute;
      box-sizing: border-box;
    }
    .percent-a{
      background: rgba(217,27,66,0.2);
      border-left: 4px solid #d91b42;
    }
    .percent-b{
      background: rgba(69,196,150,0.2);
      border-left: 4px solid #45c496;
    }
  </style>