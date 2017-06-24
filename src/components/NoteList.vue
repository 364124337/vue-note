<template>
    <div id="notes-list">
        <div id="list-header">
            <h2>Notes</h2>
            <div class="btn-group btn-group-justified" role="group" aria-label="...">
                <div class="btn-group" role="group">
                    <button :class="{active:show=='all'}" @click="show='all'" type="button" class="btn btn-default">All Notes</button>
                </div>
                <div class="btn-group" role="group">
                    <button :class="{active:show=='favorites'}" @click="show='favorites'" type="button" class="btn btn-default">Favorites</button>
                </div>
            </div>
        </div>
        <div class="container">
            <div class="list-group">
                <a :class="{active:activeNote == item}" @click="updateActiveNote(item)" v-for="item in notes" href="#" class="list-group-item" >
                    <h4 class="list-group-item-heading">
                            {{item.text}}
                    </h4>
                </a>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            show:"all"
        }
    },
    computed:{
        notes(){
            if(this.show == 'all'){
                return this.$store.getters.notes;
            }else if(this.show == 'favorites'){
                return this.$store.getters.notes.filter(note=>note.favorite);
            }
        },
        activeNote(){
            return this.$store.getters.activeNote;
        }
    },
    methods:{
        updateActiveNote(note){
            this.$store.dispatch('updateActiveNote',note);
        }
    }
}
</script>

<style type="text/html">
#notes-list {
    float: left;
    width: 300px;
    height: 100%;
    background-color: #F5F5F5;
    font-family: 'Raleway', sans-serif;
    font-weight: 400;
}

#list-header {
    padding: 5px 25px 25px 25px;
}

#list-header h2 {
    text-align: center;
    text-transform: uppercase;
    font-weight: 300;
    font-size: 22px;
    padding-bottom: 8px;
}

#notes-list .container {
    height: calc(100% - 137px);
    max-height: calc(100% - 137px);
    overflow: auto;
    width: 100%;
    padding: 0;
}
#notes-list .container .list-group-item {
  border: 0;
  border-radius: 0;
}
.list-group-item-heading {
  font-weight: 300;
  font-size: 15px;
}
</style>
