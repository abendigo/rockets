<script context="module">
  export async function load({ page, fetch, session, context}) {
    const response = await fetch(`https://api.spacexdata.com/v4/launches`);

    if (response.ok) {
      return {
        props: {
          launches: await response.json()
        }
      };
    }

    return {
      status: response.status,
			error: new Error(`Could not load https://api.spacexdata.com/v4/launches`)
    };
  }
</script>

<script>
  export let launches;

  console.log(launches[1])

  function getStatus() {
    return 'Successful';
  }
</script>

<style>
  a:link {
    text-decoration: none;
  }

  .launch {
    border: 1px solid lightgrey;
    max-width: 600px;
    margin: auto;
    display: flex;
    justify-content: space-between;
  }

  .patch {
    width: 56px;
    display: inline-block;
  }

  .details {
    display: inline-block;
    width: 70%;
  }

  .outcome {
    display: inline-block;
  }

</style>

{#each launches as { id, name, date_utc, success, links, rocket } (id)}
 <!-- <a href='/launch/{id}'>/launch/{id}</a>
 <br />
 -->
 <a href='/rocket/{rocket}'>
  <div class='launch'>
   <img class='patch' src={links.patch.small || 'static/spacex_logo_square.png'} alt='' />
   <div class='details'>
    <div class='name'>{name}</div>
    <div class='date'>{date_utc}</div>
   </div>
   <div class='outcome'>{getStatus()}</div>
  </div>
  </a>
 {/each}
