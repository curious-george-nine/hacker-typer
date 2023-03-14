<script>
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  /**
   * @param {Event & { currentTarget: EventTarget & HTMLInputElement; }} e
   */
  function handleSpeedChange(e) {
    dispatch("speedChange", {
      speed: e.currentTarget.value,
    });
  }
</script>

<div class="modal">
  <p>速度</p>
  <input
    type="range"
    min="1"
    max="15"
    value="6"
    on:change={(e) => handleSpeedChange(e)}
  />
  <p>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
    <span>|</span>
  </p>
</div>

<style>
  .modal {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 300px;
    height: 300px;
    background-image: linear-gradient(
      to bottom right,
      #808080bf,
      #707070bf,
      #404040bf 60%,
      #202020bf 90%,
      #000000bf 99%,
      #000000bf 99%
    );
    backdrop-filter: blur(2px);
    color: rgb(0, 255, 0);
    border-radius: 5px;
  }

  .modal > p + input[type="range"] {
    width: 100%;
  }

  .modal > p + input[type="range"] + p {
    width: 100%;
    display: flex;
    justify-content: space-around;
  }
</style>
