<script>
  import { FeedbackStore } from "../stores";
  import Card from "./Card.svelte";
  export let item;

  const handleDelete = (itemId) => {
    FeedbackStore.update((currentFeedback) => {
      return currentFeedback.filter((item) => item.id !== itemId);
    });
  };
</script>

<Card>
  <div class="rating-display">
    {item.rating}
  </div>
  <button class="close" on:click={() => handleDelete(item.id)}>X</button>
  <p class="text-display">
    {item.text}
  </p>
</Card>

<style>
  .rating-display {
    background: #ff6a95;
    border: 1px #eee solid;
    border-radius: 50%;
    color: #fff;
    font-size: 19px;
    left: -10px;
    padding: 10px;
    position: absolute;
    text-align: center;
    top: -10px;
    width: 50px;
    height: 50px;
  }

  .close {
    background: none;
    border: none;
    cursor: pointer;
    position: absolute;
    right: 20px;
    top: 10px;
  }
</style>
