<script lang="ts">
  import axios from 'axios'

  function sendReq() {
    const hennegeApi = axios.create({
      baseURL: "https://cors-anywhere.herokuapp.com/https://api.challenge.hennge.com/challenges/003",
      headers: {
        "Authorization": "Basic YnVkemhhbG92OTlAZ21haWwuY29tOkhFTk5HRUNIQUxMRU5HRQ==",
        "Accept": "*/*",
        "Host": "api.challenge.hennge.com",
        "Content-Type": "application/json"
      },
    })

    hennegeApi
      .post('', {
        'github_url':'https://gist.github.com/kisaragi99/7d627f6e949aa2df73e1ad9c41dfe019',
        'contact_email': 'budzhalov99@gmail.com'
      })
      .then(responce => console.log(responce))
      .catch(err => {
        console.log(err.message)
      })
  }

</script>

<style lang="scss">

</style>

<button
  on:click={() => {
    sendReq();
  }}>
  send
</button>
