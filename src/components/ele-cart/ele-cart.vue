<template>
    <div class="shop-cart">
        <div class="left">
            <div class="shop-wrap" :class="{highLight:totalPrice >0}">
                <div class="logo">
                    <i class="shopping_cart icon-shopping_cart"></i>
                </div>
                <span class="qipao" v-show="totalCount >0">{{totalCount}}</span>
            </div>
            <div class="totalPrice">
                <span :class="{highLight:totalPrice >0}">￥{{totalPrice}}</span>
            </div>
            <div class="deliveryPrice">
                <span>另需配送费￥{{deliveryPrice}}</span>
            </div>
        </div>
        <div class="right" :class="{highlight:this.totalPrice >= this.minPrice}">
            <span>{{payText}}</span>
        </div>
        <div clas="balls">
        <div class="ball-wrap" v-for="ball in balls">
            <i class="ball"></i>
        </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: "ele-cart",
        props:{
            selectedFoods:Array,
            deliveryPrice:Number,
            minPrice:Number
        },
        computed:{
            totalPrice(){
                let totalPrice =0;
                this.selectedFoods.forEach((food)=>{
                    totalPrice += (food.count * food.price)
                })
                return totalPrice
            },
            totalCount(){
                let totalCount =0;
                this.selectedFoods.forEach((food)=>{
                    totalCount += food.count
                })
                return totalCount
            },
            payText(){
                if(this.totalPrice === 0){
                    return `¥${this.minPrice}起送`
                }else if(this.totalPrice < this.minPrice){
                    return `还差¥${this.minPrice - this.totalPrice}起送`
                }else {
                    return `去结算`
                }
            }
        }
    }
</script>

<style scoped lang="stylus">
    .shop-cart
        display flex
        position fixed
        bottom 0
        left 0
        width 100%
        height 48px
        background #141d27
        .left
            display flex
            flex 1
            .shop-wrap
                display flex
                align-items center
                justify-content center
                position relative
                top -10px
                width 56px
                height 56px
                margin-left 12px
                margin-right 12px
                border-radius 50%
                background #141d27
                &.highLight
                    .logo
                        background rgba(0,160,220,1)
                        .shopping_cart
                            color rgba(255,255,255,1)
                .logo
                    display flex
                    align-items center
                    justify-content center
                    width 44px
                    height 44px
                    border-radius 50%
                    background rgba(255,255,255,.4)
                    .shopping_cart
                        font-size 24px
                        line-height 24px
                        color rgba(255,255,255,.6)
                .qipao
                    position absolute
                    right 0
                    top 0
                    width 24px
                    height 16px
                    background rgba(240,20,20,1)
                    color white
                    text-align center
                    border-radius 6px
                    box-shadow 0px 4px 8px 0px rgba(0,0,0,.4)
                    font-size 9px
                    line-height 16px
            .totalPrice
                display flex
                align-items center
                justify-content center
                span
                    display inline-block
                    border-right 1px solid rgba(255,255,255,.5)
                    padding-right 12px
                    font-size 16px
                    line-height 24px
                    color rgba(255,255,255,.4)
                    font-weight 700
                    &.highLight
                        color rgba(255,255,255,1)
            .deliveryPrice
                display flex
                align-items center
                justify-content center
                padding-left 12px
                span
                    font-size 16px
                    line-height 24px
                    color rgba(255,255,255,.4)
                    font-weight 200

        .right
            flex 0 0 105px
            background rgba(255,255,255,.4)
            display flex
            align-items center
            justify-content center
            &.highlight
                background green
                span
                    font-weight 800
                    color rgba(255,255,255,1)
            span
                color rgba(255,255,255,.6)

</style>