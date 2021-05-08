<script>
  import ingridients from "../ingridients.yaml";

  function getRandom(possibilities) {
    let random = Math.floor(Math.random() * possibilities.length);
    return possibilities[random];
  }

  function share(event) {
    let target = event.target.dataset["target"];

    let ingridients = document.querySelectorAll(
      "td[data-target=" + target + "]"
    );

    let list = "";

    for (let item of ingridients) {
      list += `${item.innerHTML}\n`;
    }

    navigator.share({ title: "Rezept", text: list });
  }
</script>

<main>
  {#each ingridients as category}
    <section>
      <h2>{Object.keys(category)}</h2>
      <table class="pure-table pure-table-vertical pure-table-striped">
        <thead
          ><tr>
            <th>Kategorie</th>
            <th>Auswahl</th>
          </tr></thead
        >
        <tbody>
          {#each Object.values(category) as ingridient, i}
            {#each Object.values(ingridient) as possibility, j}
              <tr>
                <td>
                  {Object.keys(ingridient)[j]}
                </td>
                <td data-target={Object.keys(category)}>
                  {getRandom(possibility)}
                </td>
              </tr>
            {/each}
          {/each}
        </tbody>
      </table>
      <button on:click={share} data-target={Object.keys(category)}
        >Speichern</button
      >
    </section>
  {/each}
</main>

<style>
</style>
