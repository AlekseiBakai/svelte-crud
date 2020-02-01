<script>
    import {createEventDispatcher} from 'svelte';

    const dispatch = createEventDispatcher();

    export let isEdit = false;

    let data = {
        title: '',
        category: '',
        content: '',
    };

    const onAddNote = () => {
        dispatch("addNote", data);
        data = {
            title: '',
            category: null,
            content: '',
        }
    };

    const onUpdateNote = () => {
        dispatch("updateNote");
    }

</script>

<div class="card p-2 shadow">
    <div class="card-body">
        <h5 class="card-title mb-4">Add New Note</h5>
        <form>
            <div class="form-group">
                <label for="title">Title</label>
                <input
                        bind:value={data.title}
                        type="text"
                        class="form-control"
                        id="text"
                        placeholder="Note Title"/>
            </div>
            <div class="form-group">
                <label for="category">Category</label>
                <select
                        class="form-control"
                        id="category"
                        bind:value={data.category}>
                    <option selected disaabled>Selecet a category</option>
                    <option value="Work">Work</option>
                    <option value="Home">Home</option>
                </select>
            </div>
            <div class="form-group">
                <label for="content">Content</label>
                <textarea
                        bind:value={data.content}
                        class="form-control"
                        id="content"
                        rows="3"
                        placeholder="Note Content"/>
            </div>
            {#if isEdit === false}
                <button
                        type="submit"
                        on:click|preventDefault={onAddNote}
                        class="btn btn-primary">
                    Add Note
                </button>
            {:else}
                <button
                        type="submit"
                        on:click|preventDefault={onUpdateNote}
                        class="btn btn-info">
                    Update Note
                </button>
            {/if}
        </form>
    </div>
</div>
