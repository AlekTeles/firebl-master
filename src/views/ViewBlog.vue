<template>
    <div class="post-view" v-if="currentBlog">
        <div class="container quillWrapper">
            <h2>{{ this.currentBlog[0].blogTitle }}</h2>
            <h4>Posted on: {{ new Date(this.currentBlog[0].blogDate).toLocaleString('en-us', {dateStyle: "long" }) }}</h4>
            <img :src="this.currentBlog[0].blogCoverPhoto" alt=""/>
            <div class="post-content ql-editor" v-html="this.currentBlog[0].blogHTML"></div>
        </div>
    </div>
</template>  
 
<script>
export default {
name: "ViewBlog",
data() {
    return {
        currentBlog: null,
    };
},
async mounted() {
    this.currentBlog = await this.$store.state.blogPosts.filter((post) => {
        return post.blogID === this.$route.params.blogid;
    });
  },
};
</script>

<style lang="scss" >

.post-view {   
     
    text-align: center;
    margin-bottom: 100px;
    h2 {
        margin-top: 50px;
    }
    img {
        max-width: 800px;
        max-height: 800px;
    }
    h4 {
        font-weight: 400;
        font-size: 14px;
        margin-bottom: 24px;
    }
    p {
        text-align: center;
    }
}
</style>