{#each channels as channel (channel.id)}
  <div>
    <img src={withSize(channel.thumbnail_url)} />
    viewers: {channel.viewer_count}
  </div>
{:else}
  <div>Nothing to see (yet)</div>
{/each}

<script>
  import fp from "lodash/fp";

  const user_ids = ["fextralife", "drdisrespect"];

  let channels = [];

  user_ids.forEach(id => {
    fetch("/api/helix/streams?user_login=" + id, {
      headers: {
        authorization: "Bearer 4e0naeveanx49t4kfsbdxhrrqmk7eq",
        "client-id": "hush"
      }
    })
      .then(res => res.json())
      .then(({ data }) => {
        if (data.length === 0) return;
        const [stream] = data;
        channels = fp.sortBy("viewer_count", [...channels, stream]);
      })
      .catch(e => {
        console.log(e);
      });
  });

  const withSize = url => url.replace(/\{.*?\}/g, 100);
</script>
