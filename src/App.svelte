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
  </ol>
</main>

<style>
  p.first-paragraph {
    color: orangered;
    font-size: 2em;
  }
</style>
