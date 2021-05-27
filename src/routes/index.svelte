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

  function getStatus({ success, upcoming }) {
    if (upcoming === true)
      return 'Upcoming';
    if (success === true)
      return 'Successful';
    return 'Failed';
  }

  function getStatusClass({ success, upcoming }) {
    if (upcoming === true)
      return 'upcoming';
    if (success === true)
      return 'successful';
    return 'failed';
  }
</script>

<style>
  a:link {
    text-decoration: none;
  }

  .launch {
    border-bottom: 1px solid lightgrey;
    max-width: 600px;
    margin: auto;
    display: flex;
    justify-content: space-between;
    padding: 10px;
  }

  .patch {
    width: 56px;
    height: 56px;
    display: inline-block;
  }

  .details {
    display: inline-block;
    width: 70%;
  }

  .name {
    font-size: 16px;
    font-weight: 600;  /* bold is 700 */
    color: black;
  }

  .date {
    font-size: 14px;
    font-weight: 400; /* normal */
    color: lightgray;
  }

  .outcome {
    display: inline-block;
  }

  .failed {
    color: red;
  }
  .successful {
    color: green;
  }
  .upcoming {
    color: blue;
  }

</style>

{#each launches as { id, name, date_utc, success, upcoming, links, rocket } (id)}
 <!-- <a href='/launch/{id}'> -->
 <a href='/rocket/{rocket}'>
  <div class='launch'>
   <img class='patch' src={links.patch.small || 'static/spacex_logo_square.png'} alt='' />
   <div class='details'>
    <div class='name'>{name}</div>
    <div class='date'>{date_utc}</div>
   </div>
   <div class='outcome {getStatusClass({success, upcoming})}'>{getStatus({success, upcoming})}</div>
  </div>
  </a>
 {/each}
