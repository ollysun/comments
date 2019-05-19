<template>
    <div>
        <div>
            <comment v-for="comment in comments"
                     :key="comment.id"
                     :user="user"
                     :comment="comment"
                     @comment-updated="updateComment($event)">
            </comment>
        </div>
    </div>
</template>

<script>
    import comment from './CommentItem'
    export default {
        components: {
            comment
        },
        props: {
            user: {
                required: true,
                type: Object,
            }
        },
        data: function() {
            return {
                comments: [
                    {
                        id: 1,
                        body: "How's it going?",
                        edited: false,
                        created_at: new Date().toLocaleString(),
                        author: {
                            id: 1,
                            name: 'Nick Basile',
                        }
                    },
                    {
                        id: 2,
                        body: "Pretty good. Just making a painting.",
                        edited: false,
                        created_at: new Date().toLocaleString(),
                        author: {
                            id: 2,
                            name: 'Bob Ross',
                        }
                    }
                ]
            }
        },
        methods: {
            updateComment($event) {
                let index = this.comments.findIndex((element) => {
                    return element.id === $event.id;
                });
                this.comments[index].body = $event.body;
            }
        }
    }
</script>

<style scoped>

</style>