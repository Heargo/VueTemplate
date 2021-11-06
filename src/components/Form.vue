<template>
    <div>
        <form :action="dest"  enctype="multipart/form-data" method="post">
            <slot></slot>
        </form>
    </div>
</template>
<script>
export default {
    name:"Form",
    props: {
        dest:String,
    },
    mounted() {
        var pwd=document.getElementById("pwd")
        var pwdcheck=document.getElementById("pwdcheck")
        var sub=document.querySelector("input[type='submit']")
        sub.disabled = true
        function check(){
            if(pwd.value!=pwdcheck.value){
                    pwd.classList.add("wrong")
                    pwd.classList.remove("ok")
                    pwdcheck.classList.add("wrong")
                    pwdcheck.classList.remove("ok")
            }else{
                pwd.classList.add("ok")
                pwd.classList.remove("wrong")
                pwdcheck.classList.add("ok")
                pwdcheck.classList.remove("wrong")
                sub.disabled = false

            }
            if(pwd.value==""){
                pwd.classList.remove("wrong")
                pwd.classList.remove("ok")
                pwdcheck.classList.remove("wrong")
                pwdcheck.classList.remove("ok")
                sub.disabled = true
            }
        }
        
        if(pwd!=undefined && pwdcheck!=undefined ){
            console.log("pwd check in form enable")
            pwd.addEventListener('input', () => {
               check()
            });
            pwdcheck.addEventListener('input', () => {
               check()
            });
        }
    }
}
</script>
<style lang="scss">

.wrong{
    border:2px solid $red;
}
.ok{
    border:2px solid green;
}

form{
    display:flex;
    flex-direction:column;
    align-items:center;
    max-width: 600px;
    background-color:$formbgcolor;
    border-radius:10px;
    padding:.7rem 1rem;
    div{
        display:flex;
        flex-direction:row;
        justify-content:center;
        align-items:center;
        width: 100%;
        padding:.3rem .5rem;
        margin: .3rem;
        input{
            margin: 0 .3rem;
        }

    }
    input{
        border:none;
        border-radius:6px;
        width: calc(100% - 1.6rem);
        padding:.3rem .5rem;
        margin:.3rem 0;
    }
    input[type="submit"]{
        width: auto;
        padding:.5rem .8rem;
        background-color:$orange;
        color:$dark-blue;
    }
}
    
</style>