<script lang="ts">
    import ths1440p from "../assets/data/230625-tomshardware1440p.json";
    import tpu4k from "../assets/data/230625-techpowerup4k.json";

    let data = [];
    let selected;
    let tables = [
        { id: 1, text: `Blank` },
        { id: 2, text: `Tom's Hardware 1440p 2023-06-25` },
        { id: 3, text: `TechPowerUp 4k 2023-06-25` },
    ];
    const clearTable = () => {
        var tableHeaderRowCount = 1;
        let characterTable = document.getElementById("tableInner");
        let rowCount = characterTable.rows.length;
        for (let i = tableHeaderRowCount; i < rowCount; i++) {
            characterTable.deleteRow(tableHeaderRowCount);
        }
    };
    function loadTable() {
        if (selected.id === 1) {
            data = [];
        } else if (selected.id === 2) {
            data = ths1440p;
        } else if (selected.id === 3) {
            data = tpu4k;
        }
    }
</script>

<main class="container">
    <section>
        <div class="grid">
            <select
                id="select"
                name="select"
                required
                bind:value={selected}
                on:change={loadTable}
            >
                {#each tables as table}
                    <option value={table}>
                        {table.text}
                    </option>
                {/each}
            </select>
            <label for="modelname">
                Model
                <input
                    type="text"
                    id="modelname"
                    name="modelname"
                    placeholder="Name"
                    required
                />
            </label>
            <label for="fps">
                FPS
                <input
                    type="number"
                    id="fps"
                    name="fps"
                    placeholder="0"
                    required
                />
            </label>
            <label for="cost">
                Cost
                <input
                    type="number"
                    id="cost"
                    name="cost"
                    placeholder="0"
                    required
                />
            </label>
            <button>Add</button>
        </div>
        <figure>
            <table role="grid" id="tableInner">
                <thead>
                    <tr>
                        <th scope="col">Model</th>
                        <th scope="col">FPS</th>
                        <th scope="col">Cost</th>
                        <th scope="col">Perf/Value</th>
                    </tr>
                </thead>
                <tbody>
                    {#each data as row}
                    <tr>
                        <td>{row.modelName}</td>
                        <td>{row.avgFPS}</td>
                        <td>{row.price}</td>
                        <td>{((row.avgFPS / row.price)*100).toFixed(2)}</td>
                    </tr>
                    {/each}
                </tbody>
            </table>
        </figure>
    </section>
</main>
