<template>
    <div class="container">
        <h1>Comentario</h1>
        <hr>
        <FormComment v-on:add-comment="addComment"></FormComment>
        <hr>
        <div class="list-group">
            <p v-if="comments.length <= 0">Sem comentários...</p>
            <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="comment.id">
                <span class="comment_author">Author: <strong>{{comment.name}}</strong></span>
                <p>{{comment.message}}</p>
                <a href="#" v-on:click.prevent="removeComment(index)" title="Excluir">Excluir</a>
            </div>
        </div>
    </div>
</template>

<script>
import FormComment from './FormComment';
export default {
    components: {
        FormComment
    },
    data(){
        return{
            comments: [
                // {
                //     name: 'Joe',
                //     message: 'Lorem'
                // }
            ],
        }
    },
    methods: {
        addComment(comment){
            this.comments.push(comment);
        },
        removeComment(index){
            this.comments.splice(index, 1);
        }
    },
    // cumputed , para customizar oque for exibir.
    computed: {
        allComments(){
            return this.comments.map(comment => ({
                ...comment,
                name: comment.name.trim() === '' ? 'Anonimo' : comment.name
            }))
        }
    },
    // watch monitorar a alteração em qualquer propriedade
    watch: {
        comments(val){
            console.log('val',val)
        }
    }
}
</script>