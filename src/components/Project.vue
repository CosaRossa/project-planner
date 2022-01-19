<template>
    <div class="project" :class="{done: project.complete}">
        <div class="actions">
            <h3 @click="toggleDetails">{{project.title}}</h3>
            <div class="icons">
                <span class="material-icons tick" @click="toggleComplete">done</span>
                <router-link :to="{name: 'EditProject', params: { id: project.id}}">
                    <span class="material-icons edit">edit</span>
                </router-link>
                <span class="material-icons delete" @click="deleteProject">delete</span>
            </div>
        </div>
        <div v-show="toggleDetail" class="details">
            <p>{{project.details}}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['project'],
    data(){
        return {
            toggleDetail: false,
            url: 'http://localhost:3000/projects/' + this.project.id
        }
    },
    methods: {
        toggleDetails() {
            this.toggleDetail = !this.toggleDetail
        },
        deleteProject() {
            fetch(this.url, {method: 'DELETE'})
                .then(() => this.$emit('delete', this.project.id))
                .catch(err => console.log(err.message))
        },
        toggleComplete() {
            fetch(this.url, {
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ complete: !this.project.complete })
            }).then(() => {
                this.$emit('complete', this.project.id)
            }).catch(err => console.log(err))
            }
    }
}
</script>

<style>
    .project {
        margin: 20px auto;
        background: white;
        padding: 10px 20px;
        border-radius: 4px;
        box-shadow: 1px 2px 3px rgba(0,0,0,0.05);
        border-left: 4px solid #e90074;
    }
    h3{
        cursor: pointer;
    }
    .actions {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .material-icons {
        font-size: 24px;
        margin-left: 10px;
        color: #bbb;
        cursor: pointer;
    }
    .material-icons.tick:hover {
        color: rgb(29, 150, 29);
    }
    .material-icons.edit:hover {
        color: goldenrod;
    }
    .material-icons.delete:hover {
        color: crimson;
    }
    .project.done {
    border-left: 4px solid #00ce89;
    }
    .project.done .tick {
        color: #00ce89;
    }
</style>