<script lang="ts">
  import { onMount, SvelteComponent } from "svelte";

  let text: string = "Hello, world!";
  interface cssInterface {
    color: string;
    background: string;
    font: string;
    aling: "center" | "left" | "right";
    secondFont: "monospace" | "sans-serif";
    spacing: string;
    size: string;
    weight: "200" | "300" | "400" | "500" | "600" | "700" | "800" | "900";
  }
  let css: cssInterface = {
    spacing: "2px",
    aling: "center",
    color: "linear-gradient(20deg, mediumseagreen, orange)",
    background: "#000",
    size: "50px",
    font: "roboto",
    secondFont: "sans-serif",
    weight: "500",
  };

  function reloadCss() {
    let style = document.createElement("style");
    style.innerHTML = `    
@import url('https://fonts.googleapis.com/css2?family=${css.font
      .split(" ")
      .map((e: string) => {
        e = e.toLowerCase();
        let ne = e.split("");
        ne[0] = ne[0].toUpperCase();
        return ne.join("");
      })
      .join("+")}:wght@${css.weight}&display=swap');

body {
}

.title .text {
  font-size: ${css.size};
  --color: ${css.color};
}

.title {
  font-weight: ${css.weight};
  text-aling: ${css.aling};
  font-family: "${css.font}", ${css.secondFont};
  background: ${css.background}; 
  letter-spacing: ${css.spacing};
}
    `;
    document.getElementById("css").appendChild(style);
  }

  let text_style: string = "";

  onMount(() => {
    reloadCss();
  });
</script>

<div id="css" />

<div class="title" style=""><span class="text">{text}</span></div>

<div class="custom">
  <div class="reload_section">
    <button on:click={reloadCss} class="reloadCss">Reload</button>
  </div>

    <div class="item">
      <label for="text">Text</label>
      <input
        type="text"
        bind:value={text}
        class="input"
        placeholder="Your text"
      />
    </div>
    <div class="item">
      <label for="text">Font</label>
      <input
        type="text"
        bind:value={css.font}
        class="input"
        placeholder="Font"
      />
    </div>

    <div class="item">
      <label for="text">Spacing</label>
      <input
        type="text"
        bind:value={css.spacing}
        class="input"
        placeholder="Letter spacing"
      />
    </div>

    <div class="item">
      <label for="text">Second Font</label>
      <select bind:value={css.secondFont}>
        <option value="">default</option>
        <option value="monospace">monospace</option>
        <option value="sans-serif">sans serif</option>
      </select>
    </div>

    <div class="item">
      <label for="text">Color</label>
      <input
        type="text"
        bind:value={css.color}
        class="input"
        placeholder="any valid css color"
      />
    </div>

    <div class="item">
      <label for="text">Background</label>
      <input
        type="text"
        bind:value={css.background}
        class="input"
        placeholder="any valid css color"
      />
    </div>

    <div class="item">
      <label for="text">Size</label>
      <input
        type="text"
        bind:value={css.size}
        class="input"
        placeholder="e.g. 20px, 50px, 2em, 34px"
      />
    </div>

    <div class="item">
      <label for="text">Second Font</label>
      <select bind:value={css.secondFont}>
        <option value="">default</option>
        <option value="monospace">monospace</option>
        <option value="sans-serif">sans serif</option>
      </select>
    </div>

    <div class="item">
      <label for="text">Weight</label>
      <select bind:value={css.weight}>
        <option value="200">200</option>
        <option value="300">300</option>
        <option value="400">400</option>
        <option value="500">500</option>
        <option value="600">600</option>
        <option value="700">700</option>
        <option value="800">800</option>
        <option value="900">900</option>
      </select>
    </div>


</div>

<style>
  :global(body) {
    font-family: sans-serif;
  }
  .title {

    text-align: center;
    padding: 8em 2em;
  }

  .title .text {

  background: var(--color);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  }

  .custom .reload_section {
    margin: 0.75em 0;
    position: relative;
    text-align: center;
  }

  .custom {
    gap: 1em;
    width: 100%;
    display: flex;
    flex-direction: column;
  }

  .custom .item {
    width: 100%;
    display: grid;
    grid-template-columns: 1fr 1fr;
  }

  :global(.custom .item select), .custom .item input {
    width: 100%;
  }

  .custom .item label {
    width: 100%;
    text-align: center;
    padding: 0 0.75em;
  }

  .custom button {
    cursor: pointer;
    font-size: 0.8em;
    color: #fff;
    background: hsl(270,37%,48%);
    padding: 0.5em 0.75em;
    border: none;
    border: #0002 2px solid;
    border-radius: 0.25em;
  }

  .custom .input {
    border: none;
    padding: 0.25em 0.5em;
    border-bottom: hsl(270,10%,52%) 2px solid;
    background: transparent;
    transition: border 200ms;
  }

  .custom .input:focus-within {
    outline: none;
  }

  .custom .input:focus {
    border-bottom-color: hsl(270,50%,70%);
  }
</style>
