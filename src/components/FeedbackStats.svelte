<script>
  export let ratingCount;
  export let averageRating;
</script>

<div class="feedback-stats">
  <h4>{ratingCount} Reviews</h4>
  <h4>Ratings Average: {averageRating}</h4>
</div>

<style>
  .feedback-stats {
    align-items: center;
    display: flex;
    justify-content: space-between;
  }
</style>
