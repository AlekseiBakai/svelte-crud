<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();

    export let id;
    export let category = 'Category';
    export let title = 'Title';
    export let content = 'Content';

    const onDeleteNote = () => dispatch("deleteNote", id);
    const onEditNote = () => dispatch("editNote");
</script>

<div class="card mb-3">
    <div class="card-header">{category}</div>
    <div class="card-body">
        <h5 class="card-title">{title}</h5>
        <p class="card-text">{content}</p>
        <button class="btn btn-info" on:click={onEditNote}>
            Edit
        </button>
        <button class="btn btn-danger" on:click={onDeleteNote}>
            Delete
        </button>
    </div>
</div>
