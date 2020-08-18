<template>
  <view class="container">
    <view class="top">
        <Recipe @lock="lock" v-bind:url="url" />
    </view>
    <view class="btm">
        <touchable-opacity class="button" title="Search"
            :on-press="setUrl"
        >
            <text class="btnText">
                SEARCH
            </text>
        </touchable-opacity>
        <text-input class="input" 
            v-model="ing1"
        />
        <text-input class="input" 
            v-if="ing2Render()"
            v-model="ing2"
        />
        <text-input class="input" 
            v-if="ing3Render()"
            v-model="ing3"
        />
    </view>
  </view>
</template>

<script>
import Recipe from './Recipe'

export default {
    name: 'Main',
    components: {
        Recipe
    },
    data: function() {
            return {
            ing1: '',
            ing2: '',
            ing3: '',
            url: {url: ''},
            unlock: true,
            rev: 0,
        };
    },
    methods: {
        //Hide inputs
        ing2Render() {
            if(this.ing1 === '') {
                this.ing2 = '';
                return false;
            }
            return true;
        },
        ing3Render() {
            if(this.ing1 === '' || this.ing2 === '') {
                this.ing3 = '';
                return false;
            }
            return true;
        },

        //generete and send URL, clear fields
        setUrl: function() {
            if(!this.unlock) {return}
            this.url = {url: 'http://feedm3.herokuapp.com/vue?ing1=' + this.ing1.toLowerCase() + '&ing2=' + this.ing2.toLowerCase() + '&ing3=' + this.ing3.toLowerCase() + '&nthg=' + this.rev};
            this.ing1 = '';
            this.ing2 = '';
            this.ing3 = '';
            this.rev += 1;
        },
        //Lock button
        lock: function(t) {
            this.unlock = t;
        }
    }
}
</script>

<style>
.container {
  flex: 1;
  padding-left: 15;
  padding-right: 15;
}
.input {
    margin-top: 10;
    border-color: rgb(106, 160,198);
    border-width: 1;
    border-style: solid;
    padding: 5;
    height: 40;
    border-radius: 10;
}
.button {
    margin-top: 10;
    padding: 5;
    height: 40;
    border-radius: 10;
    background-color: rgb(106, 160,198);
    align-items: center;
    justify-content: center;
}
.btnText {
    color: white;
    font-size: 16;
    line-height: 16;
    padding-top: 5;
    text-align: center;
    justify-content: center;
}
.btm {
    flex: 1;
    margin-bottom: 40;
}
.top {
    flex: 2;
}
</style>