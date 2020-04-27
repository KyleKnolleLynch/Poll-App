<script>
  import Header from "./components/Header.svelte";
  import CreatePollForm from "./components/CreatePollForm.svelte";
  import PollList from "./components/PollList.svelte";
  import Footer from "./components/Footer.svelte";
  import Tabs from "./shared/Tabs.svelte";

  //  tabs
  let items = ["Current Polls", "Add New Poll"];
  let activeItem = "Current Polls";
  const tabChange = e => {
    activeItem = e.detail;
  };

  const handleAdd = e => {
    const poll = e.detail;
    polls = [poll, ...polls];
    activeItem = 'Current Polls'
    console.log(polls);
  }

  const handleVote = e => {
    const { id, option } = e.detail;

    let copiedPolls = [...polls];
    let upvotedPoll = copiedPolls.find(poll => poll.id == id);

    if (option === 'a') {
      upvotedPoll.votesA++
    } else {
      upvotedPoll.votesB++
    }

    polls = copiedPolls;
  }
</script>

<style>
  main {
    max-width: 960px;
    margin: 3rem auto;
    padding: 0 2rem
  }
</style>

<Header />
<main>
  <Tabs {activeItem} {items} on:tabChange={tabChange} />
  {#if activeItem === 'Current Polls'}
   <PollList on:vote={handleVote} />
  {:else if activeItem === 'Add New Poll'}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />
