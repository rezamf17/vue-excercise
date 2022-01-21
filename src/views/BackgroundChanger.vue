<style>
.box{
    border-style : groove;
    border-color: black;
    width: 100%;
    height: 500px;
    text-align: center;
    transition: 0.5s ease;
}
.box-top{
    background-color: black;
    color: white;
    font-weight: bold;
}
.box-center{
    margin-top: 140px;
    background-color: black;
    width: 300px;
    height: 200px;
    margin-left:500px;
    padding-top: 50px;
    border-radius: 5px;
}
button{
    margin-top: 10px;
    color: white;
    background-color: black;
    border: 0.2em solid;
    border-radius: 7px;
    padding: 10px
}
button:hover{
    background-color: #787878;
    transition : 0.3s ease;
}
h3{
    /* background-color:black; */
    color:white;
}
input{
    text-align: center;
    font-size: 15px;
    border-radius: 5px;
}
</style>
<template>
    <div class="box" v-bind:style="{backgroundColor : color}">
        <div class="box-top">BACKGROUND CHANGER</div>
        <div class="box-center" >
            <h3>SELECT COLOR</h3>
            <input @keyup.enter="change" type="text" v-model="input" /> <br />
            <button @click="change">CHANGE</button>
        </div>
    </div>
</template>
<script>
    export default{
        data(){
            return{
                color : '#5cc48f'
            }
        },
        methods:{
            change(){
                this.color = this.input
            }
        }
    }
</script>