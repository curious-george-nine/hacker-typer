<script>
  // @ts-ignore
  import Access from "$lib/components/Access.svelte";
  // @ts-ignore
  import Settings from "$lib/components/Settings.svelte";
  import { code } from "./code";

  let speed = 6;

  /**
   * @type {HTMLTextAreaElement}
   */
  let textarea;

  function handleScrolling() {
    textarea.scrollTop = textarea.scrollHeight - textarea.clientHeight;

    console.log(textarea.scrollHeight);
  }

  let codeSplit = code.match(new RegExp(`.{1,${speed}}`, "gs")) ?? [];

  /**
   * @type {string[]}
   */
  let codeTypedArray = [];

  let codeTyped = "";

  let numberForIndexThatIncreasesWhenType = 0;

  /**
   * @param {{ detail: { speed: number; }; }} e
   */
  function handleSpeedSettings(e) {
    speed = e.detail.speed;

    console.log(speed);

    codeSplit = code.match(new RegExp(`.{1,${speed}}`, "gs")) ?? [];

    /**
     * @type {string[]}
     */
    codeTypedArray = [];

    console.log(codeSplit);

    codeTyped = "";

    numberForIndexThatIncreasesWhenType = 0;
  }

  let isDenied = false;

  let isGranted = false;

  let isSettings = false;

  /**
   * @param {KeyboardEvent & { currentTarget: EventTarget & HTMLTextAreaElement; }} e
   */
  function handleOnKeyDown(e) {
    if (e.shiftKey) {
      isDenied = !isDenied;
      isGranted = false;
      isSettings = false;
    } else if (e.altKey) {
      isGranted = !isGranted;
      isDenied = false;
      isSettings = false;
    } else if (e.ctrlKey) {
      isSettings = !isSettings;
      isGranted = false;
      isDenied = false;
    } else if (codeSplit[numberForIndexThatIncreasesWhenType]) {
      codeTypedArray.push(codeSplit[numberForIndexThatIncreasesWhenType]);
      codeTyped = codeTypedArray.join("");
      numberForIndexThatIncreasesWhenType += 1;
    }
  }
</script>

<textarea
  on:keydown={(e) => {
    handleOnKeyDown(e);
    handleScrolling();
  }}
  bind:this={textarea}
  readonly
  class={isDenied || isGranted || isSettings ? "blur" : ""}
>
  {codeTyped}
</textarea>

{#if isDenied}
  <Access {isDenied} />
{/if}

{#if isGranted}
  <Access isDenied={!isGranted} />
{/if}

{#if isSettings}
  <Settings on:speedChange={handleSpeedSettings} />
{/if}

<style>
  @import url("https://fonts.googleapis.com/css2?family=Fira+Code:wght@300;400;500;600;700&display=swap");

  :global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Fira Code", monospace;
  }

  :global(body) {
    min-height: 100vh;
  }

  textarea {
    display: block;
    width: 100%;
    height: 100vh;
    background-color: #000;
    border: none;
    resize: none;
    color: #0f0;
    outline: none;
    background-image: url($lib/assets/bg.webp);
    background-size: cover;
    background-position: 50% 50%;
    background-repeat: no-repeat;
    cursor: none;
    text-shadow: 0px 0px 15px rgba(0, 255, 0, 1);
  }

  textarea.blur {
    color: #00ff0088;
  }

  :global(body::-webkit-scrollbar) {
    display: none;
  }

  textarea::-webkit-scrollbar {
    display: none;
  }
</style>
