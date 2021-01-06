/*
To use this component, raw html must be inserted as template strings in an array. If you only include the
image URL, it will not work. To properly size the component, its parent element must be given a width and a height, because
it is responsive. 

Also, you must have at least two elements, otherwise, it will not work. 

This gives you flexibility, because you can also include links in the carousel, or any other HTML
content that your heart desires.
 */
 
 <template>
     <div class="root-element">
                <div class="carousel-wrapper">
            <div class="carousel">
                <div id="button-l" class="button-l"><i style="margin-right: 4px;" class="fas fa-chevron-left"></i></div>
                <div id="button-r" class="button-r"><i style="margin-left: 4px;" class="fas fa-chevron-right"></i></div>
                <div id="inner-container" class="inner-container">
                    <span
                    v-for="item in items"
                    :key="item"
                    class="carousel-image"
                    :class="{hidden:items[0]!=item}"
                    v-html="item"
                    ></span>
                </div>
                <div style="display:none;">
                </div> 
            </div>
            </div>
     </div>
 </template>


<script>
    export default{
        props:{
            prop:{
                default:[
                `<img src="https://images.unsplash.com/photo-1436657640247-282c9abfb832?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1053&q=80" alt="stock image">`,
                `<img src="https://images.unsplash.com/photo-1568668442512-a76afc274efb?ixlib=rb-1.2.1&ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&auto=format&fit=crop&w=1047&q=80" alt="stock image">`
                
                ]
            }
        },
        data(){
            return{
                items:this.prop
            }
        },
        mounted(){

    const innerCont = document.getElementById("inner-container")
    const btnLeft = document.getElementById("button-l")
    const btnRight = document.getElementById("button-r")

     setInterval(()=>{  
              btnRight.click()
    },5000)

    const innerContStyle = innerCont.style
    innerContStyle==5
    const length = innerCont.children.length
    length==5
    let inc = 0
    let active=true

    function toggleImages(direction){
        let i=1
        if(active){
            active=false;
            if(direction=="right"){
                if(inc==(innerCont.children.length-i)){
                    i=(-(innerCont.children.length-1))
                    }
                innerCont.children[Math.abs(inc+i)].classList.remove("hidden")
                innerCont.children[Math.abs(inc)].classList.add("fadetoleft")
                innerCont.children[Math.abs(inc+i)].classList.add("fadefromright")
                
                
            setTimeout(()=>{
                innerCont.children[Math.abs(inc)].classList.add("hidden")
                innerCont.children[Math.abs(inc)].classList.remove("fadetoleft")
                innerCont.children[Math.abs(inc+i)].classList.remove("fadefromright")
                inc+=i
                active=true
            },500)
            }else if(direction=="left"){
                if(inc<1) {
                    i=(innerCont.children.length-1)
                }
                innerCont.children[Math.abs(inc-i)].classList.remove("hidden")
                innerCont.children[Math.abs(inc)].classList.add("fadetoright")
                innerCont.children[Math.abs(inc-i)].classList.add("fadefromleft")
                

            setTimeout(()=>{
                
                innerCont.children[Math.abs(inc)].classList.add("hidden")
                innerCont.children[Math.abs(inc)].classList.remove("fadetoright")
                innerCont.children[Math.abs(inc-i)].classList.remove("fadefromleft")
                inc=Math.abs(inc-i)
                active=true
            },500)
        }
        }
    }

    btnLeft.addEventListener('click',()=>{
        toggleImages("left")
    })
    btnRight.addEventListener('click',()=>{
        toggleImages("right")
    })
    document.querySelector(".carousel").addEventListener('mouseover',()=>{
        btnRight.style.transform="scale(1.2)"
        btnLeft.style.transform="scale(1.2)"
        btnRight.style.opacity="0.85"
        btnLeft.style.opacity="0.85"
    })
    document.querySelector(".carousel").addEventListener('mouseleave',()=>{
        btnRight.style.transform="scale(1)"
        btnLeft.style.transform="scale(1)"
        btnRight.style.opacity="0.5"
        btnLeft.style.opacity="0.5"
    })
        }
    }

    
</script>



<style css scoped>
 @media only screen and (max-width: 1000px) {
        
        }

        @keyframes fadefromright {
            0%{
                transform: translateX(100%);
            }
            100%{
                transform: translateX(0px);
            }
        }
        .fadefromright{
            animation: forwards 0.5s fadefromright;
        }
        @keyframes fadefromleft {
            0%{
                transform: translateX(-100%);
            }
            100%{
                transform: translateX(0px);
            }
        }
        .fadefromleft{
            animation: forwards 0.5s fadefromleft;
        }
        @keyframes fadetoright {
            0%{
                transform: translateX(0px);
            }
            100%{
                transform: translateX(100%);
                opacity:0;
            }
        }
        .fadetoright{
            animation: forwards 0.5s fadetoright;
        }
        @keyframes fadetoleft {
            0%{
                transform: translateX(0px);
            }
            100%{
                transform: translateX(-100%);
                opacity:0;
            }
        }
        .fadetoleft{
            animation: forwards 0.5s fadetoleft;
        }

        *{
            margin:0;
            padding:0;
        }
a
        .carousel{
            width:100%;
            height:100%;
            background:black;
            position: absolute;
            overflow: hidden;
            position: absolute;;
        }
        .carousel-image{
            width:100%;
            height:100%;
            margin:0;
            padding:0;
            object-fit:cover;
            position:absolute;
            
        }
        .hidden{
           visibility: hidden;
        }
        

        .inner-container{
            height: inherit;
            overflow:visible;
            justify-items: flex-start;
            margin:0;
            padding:0;
            left:0;
            
        }
        .button-l{
            position: absolute;
            background:rgba(255, 255, 255, 0.63);
            left:0;
            top:calc(50% - 2rem);
            margin-left:1rem;
            border-radius: 50%;
            height: 3rem;
            width: 3rem;
            display: grid;
            justify-items: center;
            align-content: center;
            font-size: 2.5rem;
            cursor: pointer;
            user-select: none;
            font-weight: 900;
            z-index:10;
            transition: 0.5s;
            opacity: 0.5;
            color:black;
        }
        .button-r{
            position: absolute;
            background:rgba(255, 255, 255, 0.637);
            right:0;
            top:calc(50% - 2rem);
            margin-right:1rem;
            border-radius: 50%;
            height: 3rem;
            width: 3rem;
            display: grid;
            justify-items: center;
            align-content: center;
            font-size: 2.5rem;
            cursor: pointer;
            user-select: none;
            font-weight: 900;
            z-index:10;
            transition: 0.5s;
            opacity: 0.5;
            color:black;
        }
        .root-element{
            position: relative;
            width:100%;
            height:100%;
            background:black;
        }
</style>
