<script>
  import MovieCard from "$lib/components/MovieCard.svelte";
  let { data } = $props();

  let filterByWatchlist = $state(false);

  let movies = $derived.by(() => {
    if (filterByWatchlist) {
      let moviesFiltered = data.movies.filter(
        (movie) => movie.watchlist === true,
      );
      return moviesFiltered;
    }
    return data.movies;
  });
</script>

<p><i>Daten und Bilder generiert mit ChatGPT und DALL-E</i></p>
<div>
  <a href="/movies/create" class="btn btn-primary">Add New Movie</a>
</div>
<!-- See https://getbootstrap.com/docs/5.3/forms/checks-radios/ -->
<div class="form-check mt-3">
  <input
    class="form-check-input"
    type="checkbox"
    bind:checked={filterByWatchlist}
    id="filter"
  />
  <label class="form-check-label" for="filter">
    Show only movies on watchlist
  </label>
</div>
<div class="row mt-3">
  {#each movies as movie}
    <div class="col-sm-6 col-md-4 col-lg-3 mb-2 gx-2">
      <MovieCard {movie}></MovieCard>
    </div>
  {/each}
</div>
