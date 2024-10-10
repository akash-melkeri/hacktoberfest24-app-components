<template>
    <div class="public-style-button tw-px-[24px] tw-py-[8px] bg-transparent tw-text-center">
        <p class="tw-text-[#302d2d]  tw-text-center">
            BUTTON
        </p>
    </div>
</template>
<style>
.public-style-button {
    display: inline-block;
    background: rgb(255, 255, 255);
    text-decoration: none;
    border: 3px solid #302d2d;
    border-radius: 8px;
    margin: 10px;
    position: relative;
    color: #302d2d;
    letter-spacing: 1px;
}

.public-style-button:before {
    content: '';
    width: 25px;
    height: 25px;
    background: rgb(255, 255, 255);
    ;
    border: none;
    transform: rotate(45deg);
    position: absolute;
    border-top: 0;
    border-left: 0;
    border-bottom: 0;
    bottom: -12px;
    left: -13px;
    /* transition: all .5s ease-in; */
}

.public-style-button:hover:before {
    content: '';
    width: 0;
    height: 0;
    transform: 0;
    border-top: 0;
    border-left: 0;
    border-bottom: 0;
    bottom: -12px;
    left: -13px;
    top: auto;
    transition: all .5s ease-in;
}

.public-style-button:after {
    content: '';
    width: 25px;
    height: 25px;
    background: rgb(255, 255, 255);
    ;
    border: none;
    transform: rotate(-132deg);
    position: absolute;
    border-top: 0;
    border-left: 0;
    border-bottom: 0;
    top: auto;
    right: -13px;
    top: -12px;
    /* transition: all .5s ease-in; */

}

.public-style-button:hover:after {
    content: '';
    width: 0;
    height: 0;
    transform: 0;
    border-top: 0;
    border-left: 0;
    border-bottom: 0;
    /* top: auto; */
    right: -13px;
    top: -12px;
    /* transition-property: border; */
    transition: all .5s ease-in;
}
</style>