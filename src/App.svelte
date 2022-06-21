<script>
	import Header from "./components/Header.svelte";
	import Footer from "./components/Footer.svelte";
	import CreatePollForm from "./components/CreatePollForm.svelte";
	import PollList from "./components/PollList.svelte";
	import Tabs from "./shared/Tabs.svelte";

	// TABS
	let items = ['Current Polls', 'Add New Poll'];
	let activeItem = 'Current Polls';

	
	const handleActiveTab = (e) => {
		activeItem = e.detail;
    }
	
	// let currentPolls = [
	// 	{
	// 		id: 1,
	// 		question: 'Python or Javascript?',
	// 		answerA: 'Python',
	// 		answerB: 'Javascript',
	// 		votesA: 9,
	// 		votesB: 15,
	// 	},
	// ]

	const newPollEntry = (e) => {
		const newEntry = e.detail;
		console.log(newEntry);
		currentPolls = [newEntry, ...currentPolls];
		activeItem = "Current Polls";
	}

	const handleVote = (e) => {
		const {id, option } = e.detail;
		let copiedPolls = [...currentPolls];
		let upvotedPoll = copiedPolls.find((poll) => poll.id == id);

		if(option === 'a') {
			upvotedPoll.votesA++;
		} 
		
		if (option === 'b') {
			upvotedPoll.votesB++;
		}
		currentPolls = copiedPolls;
	}

</script>




<Header />

<main>
	<Tabs {activeItem} {items} on:tabChange={handleActiveTab} />
	
	{#if activeItem === "Current Polls"}

		<PollList on:vote={handleVote}/>
		
		{:else if activeItem === "Add New Poll"}
		
		<CreatePollForm on:AddPollEntry={newPollEntry} />

	{/if}



</main>

<Footer />



<style>
	main{
		max-width: 960px;
		margin: 40px auto;
	}
</style>