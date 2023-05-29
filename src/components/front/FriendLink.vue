<template>

    <div>
        <div class="ad whitebg imgscale">
            <ul>
                <a href="/"><img src="http://localhost:8081/cms/upload/982ec08c-2ac1-469c-8dae-99674b03acd8.jpg"></a>
            </ul>
        </div>

        <div class="links whitebg">
            <h2 class="htitle"><span class="sqlink"></span>友情链接</h2>
            <ul>
                <li v-for="(item,index) in friendLink" :key="index">
                    <a :href="item.url" target="_blank">{{item.title}}</a></li>

            </ul>
        </div>
    </div>
</template>

<script>
    import {getListLink} from "@/api/friendLink";
    export default {
        name: "FriendLink",
        data(){
            return{
                friendLink: []
            }
        },
        created() {
            getListLink().then(data=>{
                this.friendLink=data.data
            })
        }
    }
</script>

<style scoped>

</style>