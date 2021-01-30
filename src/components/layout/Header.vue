<template>
    <header class="header">
        <h2>User Data</h2>
        <div id="nav">
            <router-link to="/">Home</router-link> |
            <router-link to="/about">About</router-link>
        </div>
    </header>
</template>

<script>
export default {
    name: "Header"
}
</script>

<style scoped>
    .header {padding: 60px;text-align: center;background: #ef4232;color: white;font-size: 30px;
        background-image: url('~@/assets/img/round1.png'), url('~@/assets/img/round2.png'), url('~@/assets/img/round3.png');
        background-position: left 5% bottom 0, left 50% top 0, right 10% top 0;
        background-repeat: no-repeat;
        background-size: 131px 109px, 431px 107px, 277px 138px;
        border: 1px solid transparent;}

    #nav {padding: 30px;}

    #nav a {color: #2c3e50;text-decoration: none;}

    #nav a.router-link-exact-active { color: #ffffff;}
    
</style>