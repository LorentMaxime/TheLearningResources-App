<template>
    <div>
        <dialog open="true">
            <header>
                <slot name="header">
                    <h2></h2>
                </slot>
            </header>
            <section>
                <slot></slot>
            </section>
            <menu>
                <slot name="action"></slot>
            </menu>
        </dialog>
    </div>
</template>

<style scoped>
div {
    background-color: black;
    opacity: 0.7;
    width: 100%;
    height: 100%;
}
dialog {
    background-color: white;
    color: black;
}
</style>