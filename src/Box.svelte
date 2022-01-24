<div class="box">
  <slot name="header">No header was provided</slot>
  <p>Some content between header and footer</p>
  <slot name="footer" />
</div>

<style>
  .box {
    width: 500px;

    border: 1px solid #aaa;
    border-radius: 2em;
    box-shadow: 2px 2px 8px rgba(39, 22, 22, 0.1);
    padding: 1em;
    margin: 0 0 1em 0;

    display: flex;
    flex-direction: column;
    gap: 1em;
    background-color: rgb(175, 224, 247);
  }
</style>
