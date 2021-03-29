<template>
    <div :style = "this.boxStyle" @click="start">
    </div>
</template>
<script>
    const delay = 20 

    const sinify = (scale) => Math.sin(Math.PI * scale)
    class State {

        constructor() {
            this.scale = 0 
            this.dir = 0
        }

        update(cb) {
            this.scale += 0.02 * this.dir  
            if (Math.abs(this.scale) > 1) {
                this.scale = 0
                this.dir = 0 
                cb()
            }
        }

        startUpdating(cb) {
            if (this.dir == 0) {
                this.dir = 1
                cb()
            }
        }
    }

    class Animator {

        constructor() {
            this.animated = false 
        }

        start(cb) {
            if (!this.animated) {
                this.animated = true 
                this.interval = setInterval(cb, delay)
            }
        }

        stop() {
            if (this.animated) {
                this.animated = false 
                clearInterval(this.interval)
            }
        }
    }
    const animator = new Animator()
    export default {
        name: 'JumpBox',
        data() {
            return {
                state : new State()
                
            }
        },

        computed: {
            boxStyle() {
                const width = '100px'
                const height = '100px'
                const position = 'absolute'
                const top = `${400 * (1 - sinify(this.state.scale))}px`
                const left = '400px'
                const background = 'green'
                return {
                    width, 
                    height, 
                    position,
                    top, 
                    left, 
                    background
                }
            }   
        },
        methods: {
            start() {
                this.state.startUpdating(() => {
                    animator.start(() => {
                        this.state.update(() => {
                            animator.stop()
                        })
                    })
                })
            }
        }
    }
</script>