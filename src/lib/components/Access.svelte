<script>
  export let isDenied = false;
</script>

<div class="access {isDenied ? 'access-denied' : 'access-granted'}">
  <div class="access-inner">
    {isDenied ? "access denied" : "access granted"}
  </div>
</div>

<style>
  .access {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-transform: uppercase;
    font-size: 5rem;
    padding-inline: 2rem;
  }

  .access-denied {
    color: red;
    border-color: red;
    border-style: solid;
    border-width: 2px;
  }

  .access-granted {
    color: #0f0;
    border-color: #0f0;
    border-style: solid;
    border-width: 2px;
  }
</style>
