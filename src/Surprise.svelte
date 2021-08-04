<script>
  export let allData;
  let authors, date, start, end;

  function authorsToString(obj) {
    let _authors = [];
    obj.forEach((author) => {
      _authors.push(author.name + " from " + author.entity);
    });

    return _authors.join("\n");
  }

  $: {
    if (allData) {
      authors = authorsToString(allData.other.authors);
      date = allData.start.toLocaleDateString();
      start = allData.start.toLocaleTimeString();
      end = allData.end.toLocaleTimeString();
    }
  }
</script>

<article>
  <div class="grid">
    <div>
      <p>{authors}</p>
      {#each allData.other.authors as item, i}
        <p>{i + 1}: {item.name} x {item.entity}</p>
        {#if item.picture != undefined}
          <img src={item.picture} />
        {/if}
      {/each}
      <p>{date}</p>
      <p>{allData.other.session_type}</p>
      <p>From {start} to {end}</p>
      <p>Target audience: {allData.other.target_audience.join(", ")}</p>
      <p>Tags: {allData.other.tags.join(", ")}</p>
    </div>
    <div>
      <p>{allData.title}</p>
      {#if allData.abstract != undefined}
        <p>{allData.abstract}</p>
      {/if}
    </div>
  </div>
</article>
<p>
  🎉 {JSON.stringify(allData)} 🍾
</p>
