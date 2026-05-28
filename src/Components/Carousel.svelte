<script>
    import{flip} from 'svelte/animate';
    import Derecha from '../assets/Derecha.svg'
    import Izquierda from '../assets/Izquierda.svg'

    export let images;
    export let speed=300;

    const rotateLeft = e => {
        const transitioningImage = images[images.length -1]
        images = [images[images.length -1],...images.slice(0, images.length -1)]
    }
    const rotateRight = e => {
        const transitioningImage = images[0]
        images = [...images.slice(1, images.length), images[0]]
    }
   
    
</script>

<div id=carouselContainer>
    <div id=carouselImages>
        {#each images as image (image.id)}
            <img src={image.path} alt={image.id} id={image.id} animate:flip={{duration: speed}}/>
        {/each}
    </div>
    <button id="left" on:click={rotateLeft}>
        <slot name="=leftControl">
            <img src={Izquierda}>
        </slot>
    </button>
    <button id="right" on:click={rotateRight}>
        <slot name="=leftControl">
            <img src={Derecha}>
        </slot>
    </button>
</div>

<style>
    #carouselImages img{
        width: 100%;
    }

    #carouselContainer{
        width: calc(100%-8rem);
        height: 450px;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        position:relative;
        margin: 0rem 4rem;
          
    }

    #carouselImages{
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        align-items: center;
        flex-wrap: nowrap;
        height:100%;
        width: 100%;
        --webkit-mask: linear-gradient (to right, transparent, black 40%, black 60%, transparent);
        mask:linear-gradient (to right, transparent, black 40%, black 60%, transparent);  
    }

    button{
        position: absolute;
        top: 40%;
        transform:translateY(-50%);
        display: flex;
        align-items: center;
        justify-content: center;
        background: transparent;
        border: none;
        width: 2rem;
    }

    #left{
        left: 10px;
    }

    #right{
        right: 10px;
    }
</style>