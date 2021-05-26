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

  let { name, type, first_flight } = rocket
</script>

<style>
  .rocket {
    border: 1px solid lightgrey;
    max-width: 600px;
    margin: auto;
  }
</style>

<div class='rocket'>
  <div class='name'>Rocket Name: {name}</div>
  <div class='type'>Rocket Type: {type}</div>
  <div class='reused'>Reused: {first_flight} </div>
</div>
