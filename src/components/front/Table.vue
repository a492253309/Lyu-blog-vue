<template>
    <div class="tab_box whitebg">

        <template>
        <div class="tab_buttons">
            <ul>
                <li v-for="(item,index) in channels" :key="index"  @click="curlist(item.id)" :class="{newscurrent: cur==item.id}">{{item.name}}</li>
            </ul>
        </div>
        <div class="newstab">
            <div class="newsitem" :v-show="cur==cur">
                <div class="newspic">
                    <ul>
                        <li><router-link :to='"/detail/"+xxxx.id' target="_blank"><img src="http://localhost:8081/cms/upload/718990d5-6f8e-4f18-9a3b-ef747fea04f8.jpg"><span >{{xxxx.title}}</span></router-link></li>

                        <li><router-link :to='"/detail/"+yyyy.id' target="_blank" ><img src="http://localhost:8081/cms/upload/982ec08c-2ac1-469c-8dae-99674b03acd8.jpg"><span>{{yyyy.title}}</span></router-link></li>
                    </ul>
                </div>
                <ul class="newslist">
                    <li v-for="(item,index) in articles" :key="index"><i></i><router-link :to='"/detail/"+item.id' target="_blank">{{item.title}}</router-link>
                        <p>{{item.summary}}</p>
                    </li>
                </ul>
            </div>
        </div>
        </template>
    </div>
</template>

<script>

    import {queryByPos,getChannelArticlePos} from '@/api/front'

    export default {
        name: "Table",
        data(){
            return{
                articles:[],
                channels : [],
                xxxx: {
                    id: '',
                    title:''
                },
                yyyy: {
                    id: '',
                    title:''
                },
                cur:''
            }
        },
        mounted() {
            queryByPos('b').then(data=>{
                this.channels=data.data

            }).catch(error=>{
                this.$message.error(error)
            })
            this.curlist(this.cur)

        },methods:{
            curlist(id){
                this.cur=id
                getChannelArticlePos(id).then(data=>{
                    this.articles=data.data

                    if (data.data[0]==null){
                        this.xxxx.id=0
                        this.xxxx.title=''
                    }else {
                        this.xxxx=data.data[0]
                    }

                    if (data.data[1]==null){
                        this.yyyy.id=0
                        this.yyyy.title=''
                    }else {
                        this.yyyy=data.data[1]
                    }

                }).catch(error=>{
                    this.$message.error(error)
                })

            }
        }
    }
</script>

<style scoped>

</style>