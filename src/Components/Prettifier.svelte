<script>
  import { onMount } from "svelte";
  import formatFormula from "../Helpers/formula.js";

  export let lang = "en";

  let input = '=VLOOKUP(A1, A4:A8, (1+1)/14, False) + CONCAT(X, Y+"abc")';
  let text = formatFormula(input, lang);
  let block;

  let handleButtonGo = () => {
    text = formatFormula(input, lang);
    block.innerHTML = text;
    hljs.highlightBlock(block);
  };

  onMount(() => handleButtonGo());
</script>

<style lang="scss">
  @import "./styles/colors.scss";

  .center {
    flex-direction: column;
  }

  .white-box {
    background: $white;
    width: 60%;
    padding: 1rem;
    border: 3px solid $green-900;
    position: relative;
    z-index: 1;
  }

  @media (max-width: 900px) {
    .white-box {
      width: 90%;
    }
  }

  code {
    max-height: 100%;
  }

  img {
    max-width: 200px;
    max-height: 200px;
    position: relative;
    margin-bottom: -1.5rem;
    z-index: 2;
  }

  @media (max-height: 600px) {
    img {
      max-width: 150px;
      max-height: 150px;
    }
  }

  .row {
    display: flex;
    justify-content: left;

    #go {
      background: $green-700;
      border: 2px solid $green-900;
    }

    select {
      margin: auto 1rem;
      width: 70px;
    }
  }
</style>

<div class="center">
  <img src="./Assets/analysis.svg" alt="Excel Illustration" />
  <div class="white-box">
    {#if lang === 'de'}
      <h1>Excel Formeln Formatierer</h1>
    {:else}
      <h1>Excel Formula Prettifier</h1>
    {/if}
    <textarea bind:value={input} />
    <div class="row">
      <button type="button" id="go" on:click={handleButtonGo}>Go</button>
      <select id="lang" name="languageSelector" bind:value={lang}>
        <option value="de">de</option>
        <option value="en">en</option>
      </select>
    </div>
    <pre>
      <code class="excel" bind:this={block} />
    </pre>
  </div>
</div>
