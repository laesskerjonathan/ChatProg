<template>
    <div class="box">
        <p class="single-message" v-if="text.message">{{text.message.S}}</p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: ["text"]
}
</script>

<style scoped>
    .single-message {
        border: black 1px;
        font-size: 14.2px;
        line-height:19px;
        color:black;
        text-align: left;
    }

    .box {
        padding: 6px 7px 8px 9px;
        box-sizing:border-box;
        background-color: lightgreen;
        border-radius: 15px;
        margin: 1em;
        width: 25%;
        margin: 1em auto;
        border: 3px solid black;
        opacity: 65%;
    }

</style>