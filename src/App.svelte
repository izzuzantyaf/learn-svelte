<script lang="ts">
  import svelteLogo from "./assets/svelte.svg";
  import Nested from "./components/Nested.svelte";
  import Info from "./components/Info.svelte";

  const name = "Svelte";
  const stringHTML = "this string contains some <strong>HTML!!!</strong>";

  let count = 0;
  function incrementCount() {
    count += 1;
  }
  function decrementCount() {
    count -= 1;
  }
  $: doubled = count * 2;
  $: {
    console.log("the count is " + count);
    if (count > 0) alert("I SAID THE COUNT IS " + count);
  }
  $: if (count >= 10) {
    alert("count is dangerously high!");
    count = 9;
  }

  let numbers = [1, 2, 3, 4];
  function addNumber() {
    numbers.push(numbers.length + 1);
    numbers = numbers;
  }
  $: sum = numbers.reduce((t, n) => t + n, 0);

  let user = { loggedIn: false };

  function toggle() {
    user.loggedIn = !user.loggedIn;
  }

  const pkg = {
    name: "svelte",
    version: 3,
    speed: "blazing",
    website: "https://svelte.dev",
  };

  let x = 7;

  let cats = [
    { id: "J---aiyznGQ", name: "Keyboard Cat" },
    { id: "z_AbfPXTKms", name: "Maru" },
    { id: "OUtn3pvWmpg", name: "Henri The Existential Cat" },
  ];

  async function getRandomNumber() {
    return new Promise((resolve, reject) => {
      const number = Math.random();
      if (number > 0.5) resolve(number);
      else reject("error occured!");
    });
  }

  let promise = getRandomNumber()
    .then(res => res)
    .catch(err => err);

  function handleClick() {
    promise = getRandomNumber()
      .then(res => res)
      .catch(err => err);
  }
</script>

<main>
  <h1>Learn Svelte</h1>
  <ol>
    <li>
      <h2>Introduction</h2>
      <ol>
        <li>
          <h3>Basics</h3>
          <p>Hello world!</p>
        </li>
        <li>
          <h3>Adding data</h3>
          <p>Hello {name}!</p>
          <p>Hello {name.toUpperCase()}!</p>
        </li>
        <li>
          <h3>Dynamic attributes</h3>
          <img src={svelteLogo} alt="Svelte logo" />
        </li>
        <li>
          <h3>Styling</h3>
          <p class="first-paragraph">This is styled paragraph.</p>
        </li>
        <li>
          <h3>Nested components</h3>
          <Nested />
        </li>
        <li>
          <h3>HTML tags</h3>
          <p>{stringHTML}</p>
          <p>{@html stringHTML}</p>
        </li>
      </ol>
    </li>

    <li>
      <h2>Reactivity</h2>
      <ol>
        <li>
          <h3>Assignments</h3>
          <p>Count is {count}</p>
          <button on:click={incrementCount}> Increment count </button>
          <button on:click={decrementCount}> Decrement count </button>
        </li>
        <li>
          <h3>Declarations</h3>
          <p>{count} doubled is {count * 2}</p>
          <p>{count} doubled is {doubled}</p>
        </li>
        <li>
          <h3>Statements</h3>
          <pre>
            {`
            $: {
              console.log("the count is " + count);
              if (count > 0) alert("I SAID THE COUNT IS " + count);
            }
            $: if (count >= 10) {
              alert("count is dangerously high!");
              count = 9;
            }
            `}
          </pre>
        </li>
        <li>
          <h3>Updating arrays and objects</h3>
          <p>{numbers.join(" + ")} = {sum}</p>
          <button on:click={addNumber}> Add a number </button>
        </li>
      </ol>
    </li>

    <li>
      <h2>Props</h2>
      <ol>
        <li>
          <h3>Declaring props</h3>
          <Nested answer={42} />
        </li>
        <li>
          <h3>Default values</h3>
          <Nested />
        </li>
        <li>
          <h3>Spread props</h3>
          <Info {...pkg} />
        </li>
      </ol>
    </li>

    <li>
      <h2>Logic</h2>
      <ol>
        <li>
          <h3>If blocks</h3>
          {#if user.loggedIn}
            <button on:click={toggle}> Log out </button>
          {/if}
          {#if !user.loggedIn}
            <button on:click={toggle}> Log in </button>
          {/if}
        </li>
        <li>
          <h3>Else blocks</h3>
          {#if user.loggedIn}
            <button on:click={toggle}> Log out </button>
          {:else}
            <button on:click={toggle}> Log in </button>
          {/if}
        </li>
        <li>
          <h3>Else-if blocks</h3>
          {#if x > 10}
            <p>{x} is greater than 10</p>
          {:else if x > 5}
            <p>{x} is between 5 and 10</p>
          {:else}
            <p>{x} is less than 5</p>
          {/if}
        </li>
        <li>
          <h3>Each blocks</h3>
          <ul>
            {#each cats as cat}
              <li>
                <a
                  target="_blank"
                  href="https://www.youtube.com/watch?v={cat.id}"
                  rel="noreferrer"
                >
                  {cat.name}
                </a>
              </li>
            {/each}
          </ul>
        </li>
        <li>
          <h3>Await blocks</h3>
          <button on:click={handleClick}> generate random number </button>
          {#await promise}
            <p>...waiting</p>
          {:then number}
            <p>The number is {number}</p>
          {:catch error}
            <p style="color: red">{error}</p>
          {/await}
        </li>
      </ol>
    </li>
  </ol>
</main>

<style>
  p.first-paragraph {
    color: orangered;
    font-size: 2em;
  }
</style>
