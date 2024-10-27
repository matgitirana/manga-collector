<script lang="ts">
  import PocketBase from 'pocketbase'
  import { onMount } from 'svelte'
  import { Series } from '../domain/series'

  const pb = new PocketBase('http://127.0.0.1:8090')

  let results: Series[] = []

  onMount(async () => {
    await update()
  })

  async function update() {
    results = await pb.collection('series').getFullList()
  }
</script>

<div class="p-8 text-center">
  <h1 class="text-2xl">Bem vindo ao Manga Collector</h1>
  <p>Onde você pode registrar e manter sua coleção de mangás em dia!</p>

  <div class="mb-2 mt-5 flex items-center justify-center gap-2">
    <h2 class="text-xl">Séries disponíveis:</h2>
    <button on:click={update}>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        height="24px"
        viewBox="0 -960 960 960"
        width="24px"
        fill="#e8eaed"
        ><path
          d="M160-160v-80h110l-16-14q-52-46-73-105t-21-119q0-111 66.5-197.5T400-790v84q-72 26-116 88.5T240-478q0 45 17 87.5t53 78.5l10 10v-98h80v240H160Zm400-10v-84q72-26 116-88.5T720-482q0-45-17-87.5T650-648l-10-10v98h-80v-240h240v80H690l16 14q49 49 71.5 106.5T800-482q0 111-66.5 197.5T560-170Z"
        /></svg
      >
    </button>
  </div>
  {#each results as series}
    <p>{series.id} - {series.name}</p>
  {/each}
</div>
