<script>
  import { onMount } from 'svelte';
  import axios from 'axios';

  let flag = '';
  let countryName = '';
  let answerVisible = false;

  async function getRandomFlag() {
    try {
      const response = await axios.get(
        'https://restcountries.com/v3.1/region/asia'
      );
      const countries = response.data;
      const randomIndex = Math.floor(Math.random() * countries.length);
      const randomCountry = countries[randomIndex];

      flag = randomCountry.flags.png;
      countryName = randomCountry.name.common;
      answerVisible = false;
      console.log('WORKING!');
    } catch (error) {
      console.error('ERROR!');
    }
  }

  function revealAnswer() {
    answerVisible = true;
  }

  function newGame() {
    getRandomFlag();
  }
  onMount(getRandomFlag);
</script>

<main>
  <div class="flag-container">
    {#if flag}
      {#if answerVisible}
        <img src={flag} alt="Flag" />
        <h3>{countryName}</h3>
      {:else}
        <img src={flag} alt="Flag" />
      {/if}
    {:else}
      <p>Loading...</p>
    {/if}
  </div>
  <div class="answer-container" />
  <button on:click={revealAnswer} disabled={answerVisible}>Reveal Answer</button
  >
  <br />
  <button on:click={newGame}>New Game</button>
</main>
