<script>
  export let name;
  export let initialCounter = 2;
  let counter = initialCounter;
  const increment = () => {
    counter++
  };

  $: isEvenOrOdd = counter % 2 === 0 ? "even": "odd";


</script>

<div>
  <button on:click={increment}>
    count is {counter} {name} {initialCounter}
  </button>
  <span>{isEvenOrOdd}</span>
</div>

