<script context="module">
  export async function load({ page, fetch }) {
    const response = await fetch(`https://api.spacexdata.com/v4/rockets/${page.params.id}`);

    return {
      props: {
        rocket: await response.json()
      }
    }
  }
</script>

<script>
  export let rocket;

  let { name, type } = rocket;
</script>

<style>
  .rocket {
    border-bottom: 1px solid lightgrey;
    max-width: 600px;
    margin: auto;
    padding: 10px;
  }

  .name {
    font-size: 18px;
  }

  .type, .reused {
    font-size: 14px;
    color: lightgray;
  }
</style>

<div class='rocket'>
  <div class='name'>Rocket Name: {name}</div>
  <div class='type'>Rocket Type: {type}</div>
  <div class='reused'>Reused: unknown </div>
</div>
