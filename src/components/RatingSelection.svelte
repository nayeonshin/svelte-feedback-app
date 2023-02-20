<script>
  import { createEventDispatcher } from "svelte";

  const options = [];
  const maxRating = 10;

  let selectedOption = 10;

  const dispatch = createEventDispatcher();

  for (let i = 1; i <= maxRating; i++) {
    options.push(i);
  }

  const handleChange = (e) => {
    selectedOption = e.currentTarget.value;
    dispatch("select-rating", selectedOption);
  };
</script>

<ul class="rating">
  {#each options as option}
    <li>
      <input
        checked={selectedOption === option}
        id={option}
        name="rating"
        on:change={handleChange}
        type="radio"
        value={option}
      />
      <label for={option}>{option}</label>
    </li>
  {/each}
</ul>

<style>
  .rating {
    align-items: center;
    display: flex;
    justify-content: space-around;
    margin: 30px 0;
  }

  .rating li {
    background: #f4f4f4;
    border: 1px #eee solid;
    border-radius: 50%;
    font-size: 19px;
    height: 50px;
    padding: 10px;
    position: relative;
    text-align: center;
    transition: 0.3s;
    width: 50px;
  }

  .rating li label {
    border-radius: 50%;
    cursor: pointer;
    height: 50px;
    left: 50%;
    padding: 10px;
    position: absolute;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 50px;
  }

  .rating li:hover {
    background: #ff6a95;
    color: #fff;
  }

  /* Makes actual radio select invisible */
  [type="radio"] {
    opacity: 0;
  }

  /* Uses the sibling select */
  [type="radio"]:checked ~ label {
    background: #ff6a95;
    color: #fff;
  }
</style>
