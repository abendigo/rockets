<script context="module">
  export async function load({ page, fetch }) {
    const url = `https://api.spacexdata.com/v4/launches/${page.params.id}`;
    const response = await fetch(url);

    if (response.ok) {
      return {
        props: {
          launch: await response.json()
        }
      }
    }

    return {
      status: response.status,
			error: new Error(`Could not load ${url}`)
    };
  }
</script>

<script>
  export let launch;

  console.log({launch})
</script>

<!-- <span class='name'>Rocket Name: {name}</span>
<span class='type'>Rocket Type: {type}</span>
<span class='reused'>Reused: {first_flight} </span> -->
