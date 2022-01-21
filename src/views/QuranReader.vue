<style>
@font-face
	{
		font-family : "Arab";
		src :('../src/assets/font/ScheherazadeNew-Bold.ttf');
	}
    .font-arab{
        font-family : "Arab";
		font-size : 36px;
        text-align:right;
    }
 select{
    font-size: 18px;
    color: white;
    background: black;
    border: 0.2em solid;
    border-radius: 5px;
    width: 260px;
 }
 .chooser{
     background-color: black;
     padding: 15px 0px 15px 0px;
 }
 .info{
     text-align: right;
 }
 .search-input{
     margin: 10px 0px 10px 0px;
     color: white;
     background: black;
     border: 0.1em solid;
     font-size: 18px;
     width: 260px;
 }
 table, th, td{
     border-style: solid;
    border-collapse: collapse;
    border-color: black;
 }
 td{
     text-align:left;
 }
</style>
<template>
<div class="chooser">
    <select name="" v-model="nilai">
        <option value="">Pilih Surat</option>
        <option v-for="read in posts.data" :key="read.nomor" v-bind:value="read.nomor">{{read.nomor}}. {{read.nama}}</option>
    </select> <br />
    <input type="text" class="search-input" placeholder="Search" v-model="search"> <br /> 
    <button @click="pilihSurah">Pilih Surat</button>
</div>
    <table v-if="nilai != ''">
        <thead>
            <th>Nomor Ayat</th>
            <th>Terjemahan</th>
            <th>Ayat</th>
        </thead>
        <tbody v-for="ayat in viewSurah.data" :key="ayat.nomor">
            <td>{{ayat.nomor}}</td>
            <td>{{ayat.id}}</td>
            <td class="font-arab">{{ayat.ar}}</td>
        </tbody>
    </table>
</template>
<script>
const axios = require('axios').default;
    export default{
        data(){
            return{
                data : [
                    {id : 1, nama : 'Males', alamat : 'Jalan Garuda Pancasila Nomor 9'},
                    {id : 2, nama : 'Agak Males', alamat : 'Jalan Gangsing Nomor 2'},
                    {id : 3, nama : 'Biasa Aja', alamat : 'Jalan Semarang Nomor 932'},
                    {id : 4, nama : 'Rajin', alamat : 'Jalan Aji Masaid Nomor 19'},
                    {id : 5, nama : 'Sangat Rajin', alamat : 'Jalan Burangrang Nomor 123'}
                ],
                posts : [],
                alamat : '',
                viewSurah : false,
                nilai : '',
                search : ''
            }
        },
        methods:{
            dataSurah(){
                axios
                    .get('https://api-alquranid.herokuapp.com/surah/')
                    .then(response => (this.posts = response.data))
                },
            pilihSurah(){
                 axios
                    .get('https://api-alquranid.herokuapp.com/surah/' + this.nilai)
                    .then(response => (this.viewSurah = response.data))
            }
            
        },
        created(){
            this.dataSurah()
            this.pilihSurah()
        },
        computed:{
            filter: function(){
                return this.viewSurah.filter((ayat) => {
                    return ayat.viewSurah.nomor.match(this.search)
                })
            }
        }
    }
</script>