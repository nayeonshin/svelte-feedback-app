<script>
  import { v4 as uuidv4 } from "uuid";

  import { FeedbackStore } from "../stores";

  import Button from "./Button.svelte";
  import Card from "./Card.svelte";
  import RatingSelection from "./RatingSelection.svelte";

  const minTextCount = 10;

  let rating = 10;
  let isDisabled = true;
  let text = "";
  let message;

  const handleSelect = (e) => (rating = e.detail);
  const handleInput = () => {
    if (text.trim().length <= minTextCount) {
      message = `Text must be at least ${minTextCount}`;
      isDisabled = true;
    } else {
      message = null;
      isDisabled = false;
    }
  };
  const handleSubmit = () => {
    if (text.trim().length > minTextCount) {
      const newFeedback = {
        id: uuidv4(),
        text,
        rating: +rating,
      };

      FeedbackStore.update((currentFeedback) => {
        return [newFeedback, ...currentFeedback];
      });

      text = "";
    }
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmit}>
    <RatingSelection on:select-rating={handleSelect} />
    <div class="input-group">
      <input
        bind:value={text}
        on:input={handleInput}
        placeholder="Tell us something that keeps you coming back"
        type="text"
      />
      <Button disabled={isDisabled} type="submit">Send</Button>
    </div>
    {#if message}
      <div class="message">
        {message}
      </div>
    {/if}
  </form>
</Card>

<style>
  header {
    margin: auto;
    max-width: 400px;
  }

  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }

  .input-group {
    border: 1px solid #ccc;
    border-radius: 8px;
    display: flex;
    flex-direction: row;
    margin-top: 15px;
    padding: 8px 10px;
  }

  input {
    border: none;
    flex-grow: 2;
    font-size: 16px;
  }

  input:focus {
    outline: none;
  }

  .message {
    color: rebeccapurple;
    padding-top: 10px;
    text-align: center;
  }
</style>
