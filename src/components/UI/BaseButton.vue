<template>
    <!-- with the mode prop, idea is to use this base-button with the mode='flat' later, which is link to a css class for an alternative look -->
    <button :class="mode"> 
        <!-- with slot instead of a {{ text }} here, idea is to give the dev maximum flexibility: add a text but more: svg icon, any markup ... -->
        <slot></slot>
    </button>
</template>

<script>
    export default {
        props: ['mode']
    }
</script>

<style scoped>
    button {
    padding: 0.75rem 1.5rem;
    font-family: inherit;
    font-weight: 500;
    background-color:  	#ffe1ba;
    border: 1px solid #ffe1ba;
    color:  #8b5c29;
    border-radius: 5px;
    cursor: pointer;
    }

    button:hover,
    button:active {
    background-color: #8b5c29;
    border-color:  	#8b5c29;
    color: white;
    }

    .flat {
    background-color: transparent;
    color: #8b5c29;
    border: none;
    }

    .flat:hover,
    .flat:active {
    background-color: #ffe1ba;
    color: #8b5c29;
    }
</style>