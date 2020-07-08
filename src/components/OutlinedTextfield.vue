<template>
    <div class="textfield-container" :class="{'filled': filled}">
        <input type="text" class="textfield" v-model="content">
        <p class="textfield-label">Username</p>
    </div>
</template>

<script>
export default {
    props: {
        value: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            filled: false
        }
    },
    computed: {
        content: {
            get() {
                return this.value
            },
            set(newValue) {
                this.$emit('input',newValue)
            }
        }
    },
    mounted() {
        const children = this.$el.childNodes;
        const label = children[1];

        //Determine the background color of the label
        const elStyles = getComputedStyle(label.parentElement.parentElement.parentElement);
        label.style.backgroundColor = elStyles.backgroundColor;

        //Establish input blur event listener
        children[0].addEventListener('blur', (event) => {
            this.checkState();
        })
        //In case data is prefilled
        this.checkState(true)

        //focus input when label is clicked
        children[1].addEventListener('click', (event) => {
            children[0].focus();
        })
    },
    methods: {
        checkState(created = false) {
            const children = this.$el.childNodes
            //transition duration variable
            const transitionDuration = '250ms';

            if (children[0].value !== '') {
                if (created == true) {
                    this.filled = true;
                    setTimeout(() => {
                        children[1].style.transitionDuration = transitionDuration;
                    }, 10)
                } else {
                    this.filled = true;
                    children[1].style.transitionDuration = transitionDuration;
                }
            } else {
                this.filled = false;
                children[1].style.transitionDuration = transitionDuration;
            }
        }
    }
}
</script>

<style scoped>
    .textfield-container {
        width: 100%;
        height: 56px;
        position: relative;
        background-color: transparent;
        margin: 10px 0;
    }

    .textfield-container:hover {
        cursor: text;
    }

    .textfield-container .textfield {
        width: calc(100% - 34px);
        height: 54px;
        padding: 0 16px;
        margin: 0;
        border: 1px solid #9E9E9E;
        border-radius: 6px;
        font-size: 1rem;
        background-color: transparent;
    }

    .textfield-container .textfield:focus {
        border: 2px solid #4285F4;
        outline: none;
        width: calc(100% - 36px);
        height: 52px;
    }

    .textfield-container .textfield-label {
        padding: 0 4px;
        margin-left:-4px;
        position: absolute;
        left: 17px;
        top: 4px;
        font-size: 1rem;
        transition-property: left,top,font-size,color;
    }

    .textfield-container:focus-within .textfield-label {
        left: 18px;
        top: -16px;
        font-size: 11px;
        color: #4285F4;
        z-index:1;
    }

    .textfield-container.filled .textfield-label {
        left: 18px;
        top: -16px;
        font-size: 11px;
    }
</style>