<template>
    <div :class="classes" :style="styles">
        <slot></slot>
    </div>
</template>
<script type="text/babel">

    import {oneOf} from 'utils/assist';

    const prefixCls = 'ivu-row';

    export default {
        name: 'Row',
        props: {
            gutter: {
                type: Number,
                default: 0
            },
            type: {
                validator (value) {
                    return oneOf(value, ['flex']);
                }
            },
            justify: {
                validator (value) {
                    return oneOf(value, ['start', 'end', 'center', 'space-around', 'space-between']);
                }
            },
            align: {
                validator (value) {
                    return oneOf(value, ['top', 'middle', 'bottom']);
                }
            },
            className: String
        },
        computed: {
            classes(){
                return [
                    {
                        [`${prefixCls}`]:!this.type,
                        [`${prefixCls}-${this.type}`]:!!this.type,
                        [`${prefixCls}-${this.type}-${this.justify}`]:this.justify,
                        [`${prefixCls}-${this.type}-${this.align}`]:this.align,
                        [`${this.className}`]: !!this.className
                    }
                ];
            },
            styles(){
                let style = {};
                if (this.gutter !== 0) {
                    style = {
                        marginLeft: this.gutter / -2 + 'px',
                        marginRight: this.gutter / -2 + 'px'
                    };
                }
                return style;
            }
        },
        methods: {
            updateGutter(val){
                this.$children.forEach((child)=>{
                    if(val != 0){
                        child.gutter = val ;
                    }
                });
            }
        },
        watch: {
            gutter (val) {
                this.updateGutter(val);
            }
        }
    };
</script>