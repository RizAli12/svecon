<script>
  import Todo from "./Todo.svelte";
  import Box from "./Box.svelte";
  import AudioPlayer from "./AudioPlayer.svelte";
  let user = {
    firstname: "Ada",
    lastname: "Lovelace",
  };

  import { onMount } from "svelte";

  let characters = ["🥳", "🎉", "✨"];

  let confetti = new Array(100)
    .fill()
    .map((_, i) => {
      return {
        character: characters[i % characters.length],
        x: Math.random() * 100,
        y: -20 - Math.random() * 100,
        r: 0.1 + Math.random() * 1,
      };
    })
    .sort((a, b) => a.r - b.r);

  onMount(() => {
    let frame;

    function loop() {
      frame = requestAnimationFrame(loop);

      confetti = confetti.map((emoji) => {
        emoji.y += 0.7 * emoji.r;
        if (emoji.y > 120) emoji.y = -20;
        return emoji;
      });
    }

    loop();

    return () => cancelAnimationFrame(frame);
  });

  let todos = [
    { id: 1, done: true, text: "wash the car" },
    { id: 2, done: false, text: "take the dog for a walk" },
    { id: 3, done: false, text: "mow the lawn" },
    { id: 4, done: false, text: "Water the Plants" },
  ];

  function toggle(toggled) {
    todos = todos.map((todo) => {
      if (todo === toggled) {
        // return a new object
        return {
          id: todo.id,
          text: todo.text,
          done: !todo.done,
        };
      }

      // return the same object
      return todo;
    });
  }
</script>

<svelte:head>
  <link rel="stylesheet" href="/tutorial/dark-theme.css" />
</svelte:head>

<main>
  <div class="container2">
    <input bind:value={user.firstname} />
    <input bind:value={user.lastname} />

    {@debug user}

    >

    <h1>Hello {user.firstname}!</h1>
    <h1>Hello {user.lastname}!</h1>
  </div>

  <div class="container">
    <h1>Hello world!</h1>
  </div>

  <div class="container1">
    <h2>Todos</h2>
    {#each todos as todo}
      <Todo {todo} on:click={() => toggle(todo)} />
    {/each}
  </div>

  <Box>
    <svelte:fragment slot="footer">
      <p>All rights reserved.</p>
      <p>Copyright (c) 2019 Svelte Industries</p>
    </svelte:fragment>
  </Box>

  <!-- https://musopen.org/music/9862-the-blue-danube-op-314/ -->
  <AudioPlayer
    src="https://sveltejs.github.io/assets/music/strauss.mp3"
    title="The Blue Danube Waltz"
    composer="Johann Strauss"
    performer="European Archive"
  />

  <!-- https://musopen.org/music/43775-the-planets-op-32/ -->
  <AudioPlayer
    src="https://sveltejs.github.io/assets/music/holst.mp3"
    title="Mars, the Bringer of War"
    composer="Gustav Holst"
    performer="USAF Heritage of America Band"
  />

  <!-- https://musopen.org/music/8010-3-gymnopedies/ -->
  <AudioPlayer
    src="https://sveltejs.github.io/assets/music/satie.mp3"
    title="Gymnopédie no. 1"
    composer="Erik Satie"
    performer="Prodigal Procrastinator"
  />

  <!-- https://musopen.org/music/2567-symphony-no-5-in-c-minor-op-67/ -->
  <AudioPlayer
    src="https://sveltejs.github.io/assets/music/beethoven.mp3"
    title="Symphony no. 5 in Cm, Op. 67 - I. Allegro con brio"
    composer="Ludwig van Beethoven"
    performer="European Archive"
  />

  <!-- https://musopen.org/music/43683-requiem-in-d-minor-k-626/ -->
  <AudioPlayer
    src="https://sveltejs.github.io/assets/music/mozart.mp3"
    title="Requiem in D minor, K. 626 - III. Sequence - Lacrymosa"
    composer="Wolfgang Amadeus Mozart"
    performer="Markus Staab"
  />
  <div class="container">
    {#each confetti as c}
      <span style="left: {c.x}%; top: {c.y}%; transform: scale({c.r})"
        >{c.character}</span
      >
    {/each}
  </div>
</main>

<style>
  h2 {
    font-size: 2em;
    font-weight: bold;
    text-shadow: 2em;
  }
  main {
    background-color: darkgrey;
    text-align: center;
  }
  .container {
    background-color: pink;
    align-content: center;
    max-width: 25%;
    float: left;
    border-radius: 2em;
    box-shadow: 2px 2px 8px rgba(39, 22, 22, 0.1);
  }
  .container1 {
    background-color: rgb(240, 243, 197);
    align-content: center;
    width: 50%;
    float: right;
    padding: 4px color red;
    border-radius: 2em;
    box-shadow: 2px 2px 8px rgba(39, 22, 22, 0.1);
  }

  .container2 {
    background-color: rgb(197, 243, 235);
    float: center;
    width: 100%;
    padding: 4px color red;
    border-radius: 2em;
    box-shadow: 2px 2px 8px rgba(39, 22, 22, 0.1);
  }

  :global(main) {
    overflow: hidden;
  }

  span {
    position: absolute;
    font-size: 5vw;
    user-select: none;
  }
</style>
