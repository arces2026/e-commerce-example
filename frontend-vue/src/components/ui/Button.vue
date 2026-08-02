<template>
    <button class="fancy">
        <slot></slot>
    </button>
</template>

<style>
    .fancy{
        padding: 10px;
        background-color: var(--color-primary);
        color: var(--color-foreground);
        cursor: pointer;
        width: 200px;
        margin: 40px auto;
        border-radius: 10px;
        font-size: 1.5rem;
        transition: all 0.2s ease;
    }

    .fancy:hover {
        scale: 1.05;
        background-color: var(--color-primary-hover);
        color: rgb(240, 225, 211);
    }

    .fancy:active {
        scale: 0.95;
    }
</style>