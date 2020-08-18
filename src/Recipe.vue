<template>
    <view class="container">
        <scroll-view>
            <view class="bg" v-if="recp.length < 2">
                <text class="textL">
                    {{recp[0].top}}
                </text>
                <text class="text">
                    {{recp[0].dis}}
                </text>
            </view>
            <view v-else>
                <recp-item
                    v-for="(r, i) in recp"
                    :key="i"
                    :topic="r.top"
                    :aidi="i"
                    @setRecp="setRecp"
                />
            </view>
        </scroll-view>
    </view>
</template>

<script>
import Recps from './Recps'
export default {
    components: { 'recp-item': Recps },
    props: {
        url: {type: Object},
        lock: {type: Function}
    },
    data: function() {
        return {
            recp: [{
                top: 'Welcome to our cooking book!!!',
                dis: 'You can find any recipe you want using up to 3 ingredients!!! Unfortunately, you can use only 6 ingredients: potato, rice, tomatoes, cream, meat and paprika.'
            }],
        };
    },
    watch: {
        url: function(oldUrl, newUrl) {
            this.goFetch()
        },
    },
    methods: {
        goFetch: function() {
            this.$emit('lock', false);
            this.recp = [{
                top: 'Loading...',
                dis: 'Wait a minute... What we are doing here is not cooking at all :)'
            }]
            fetch(this.url.url)
            .then(res => res.json())
            .then(json => {
                this.recp = json;
                this.$emit('lock', true);
            });
        },
        setRecp: function(id) {
            this.recp = [this.recp[id]];
        }
    }
}
</script>

<style>
.bg {
    background-color: rgb(217, 231, 240);
    border-radius: 10;
    justify-content: center;
    padding: 10;
}
.text {
    font-size: 16;
    text-align: left;
}
.textL {
    font-size: 19;
    font-weight: bold;
    text-align: left;
    margin-bottom: 5;
}
</style>