<template>
    <div>
        <div v-show="state==='default'">
            <div>
                <p>{{comment.body}}</p>
                <button v-if="editable" @click="state = 'editing'">Edit</button>
            </div>
            <div>
                <p>{{comment.author.full_name}} <span>&bull;</span>{{ comment.created_at}}</p>
            </div>
        </div>
        <div v-show="state==='editing'">
            <div>
                <h3>Update Comment</h3>
            </div>
            <textarea v-model="data.body"
                      placeholder="Update comment"
                      class="border">
            </textarea>
            <div>
                <button @click="saveEdit">Update</button>
                <button @click="resetEdit">Cancel</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            user: {
                required: true,
                type: Object,
            },
            comment: {
                required: true,
                type: Object,
            }
        },
        computed: {
            editable() {
                return this.user.id === this.comment.author.id;
            }
        },
        data: function() {
            return {
                state: 'default',
                data: {
                    body: this.comment.body,
                }
            }
        },
        methods: {
            resetEdit() {
                this.state = 'default';
                this.data.body = this.comment.body;
            },
            saveEdit() {
                this.state = 'default';
                this.$emit('comment-updated', {
                    'id': this.comment.id,
                    'body': this.data.body,
                });
            }
        }
    }
</script>

<style scoped>

</style>