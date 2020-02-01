<script>
    import Card from './components/Card.svelte';
    import AddCard from './components/AddCard.svelte';

    let notes = [
        {
            id: 1,
            title: 'Sweetest framework ever',
            category: 'Home',
            content: 'This is the content of this note',
        },
        {
            id: 2,
            title: 'intro to svelt',
            category: 'Work',
            content: 'This could be an intro to svelt,so you need to keep calm and see the magic',
        },
    ];

    let data = {
        title: '',
        category: '',
        content: '',
        id: null,
    };

    let addNote = ({detail}) => {
        const newPlayer = Object.assign(detail, {id: notes.length + 1});
        notes = [...notes, newPlayer];
    };

    let isEdit = false;

    let editNote = note => {
        isEdit = true;
        data = note;
    };

    let updateNote = () => {
        isEdit = !isEdit;

        let noteDB = {
            title: data.title,
            category: data.category,
            content: data.content,
            id: data.id,
        };

        let objIndex = notes.findIndex(obj => obj.id == noteDB.id);

        notes[objIndex] = noteDB;
        data = {
            id: null,
            title: '',
            category: '',
            content: '',
        };
    };

    let deleteNote = ({detail}) => {
        notes = notes.filter(note => note.id !== detail);
    };
</script>
<style>
    @import url("https://fonts.googleapis.com/css?family=Nunito&display=swap");

    * {
        font-family: "Nunito", sans-serif;
    }
</style>
<section>
    <div class="container">
        <div class="row mt-5 ">
            <div class="col-md-6">
                <AddCard on:addNote={addNote} on:updateNote={updateNote} isEdit={isEdit}/>
            </div>
            <div class="col-md-6">
                {#if notes.length === 0}
                    <div class="alert alert-danger text-center" role="alert">
                        No notes
                    </div>
                {:else}
                    {#each notes as note}
                        <Card
                                {...note}
                                on:deleteNote={deleteNote}
                                on:editNote={editNote(note)}/>
                    {/each}{/if}
            </div>
        </div>
    </div>
</section>
