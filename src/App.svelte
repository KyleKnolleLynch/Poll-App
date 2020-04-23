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

  //  polls
  let polls = [
    {
      id: 1,
      question: 'Python or Javascript?',
      answerA: 'Python',
      answerB: 'Javascript',
      votesA: 9,
      votesB: 22
    },
  ];

  const handleAdd = e => {
    const poll = e.detail;
    polls = [poll, ...polls];
    activeItem = 'Current Polls'
    console.log(polls);
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
   <PollList {polls} />
  {:else if activeItem === 'Add New Poll'}
    <CreatePollForm on:add={handleAdd} />
  {/if}
</main>
<Footer />
