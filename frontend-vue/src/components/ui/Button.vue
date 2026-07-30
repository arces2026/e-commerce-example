<template>
    <button class="fancy">
        <slot></slot>
    </button>
</template>

<style>
    .fancy{
        padding: 10px;
        background-color: bisque;
        color: rgb(172, 103, 34);
        cursor: pointer;
        width: 200px;
        margin: auto;
        border-radius: 10px;
        font-size: 1.5rem;
        transition: all 0.3s ease;
    }

    .fancy:hover {
        scale: 1.05;
        background-color: rgb(196, 143, 80);
        color: rgb(240, 225, 211);
    }

    .fancy:active {
        scale: 0.95;
    }
</style>