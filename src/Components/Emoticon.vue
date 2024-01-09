<script setup>
import { ref , computed, watch } from 'vue'
import EmojiList from '../emojis'
const emit = defineEmits(['clickEmoticon'])

const props = defineProps([''])
let categories = Object.keys(EmojiList)
const enVracs = {}
const search = ref('')
const emo = ref('')
const emojiList = ref([])
const isShow = ref(false)

watch(isShow, () => {
    emojiList.value = []
})

categories.forEach(category => {
    let emojis = EmojiList[category]
    for(let key in emojis) {
        enVracs[key] = emojis[key]
    }
})

const Filtered = (mysearch) => {
    let allKeys = Object.keys(enVracs)
    return allKeys.filter((key) => key.startsWith(mysearch))
}

const getKeyCategory = (category) => {
    let allKeys = Object.keys(EmojiList[category])
    return allKeys;
}

function ChooseOne(name) {
    emo.value = enVracs[name]
    emojiList.value.push(`:${name}:`)
    
    if (props.debug != undefined)
        console.log(name, emojiList.value)

    emit('clickEmoticon', selectedEmo())
}

function toEmoji() {
    let emo = emojiList.value.map(emo => enVracs[emo.replace(':','')]).join(' ')
    console.log(emojiList.value)
    return emo
}

function toEmojiString() {
    return emojiList.value.join(' ')
}

function selectedEmo() {
    return emo.value
}

function toggleShow() {
    isShow.value = ! isShow.value
}

defineExpose({
    toEmoji,
    toEmojiString,
    toggleShow,
})
</script>
<template>
    <div v-click-outside="toggleShow" v-if="isShow" class="emoji-wrapper">
        <div class="emoji-header">
            <!-- <h6>List of emoji</h6> -->
            <input placeholder="Search emoji" class="emoji-search-input" v-model="search" type="search">
        </div>
        <div class="emoji-smeiley-list">
            <div class="emoji-category" v-for="category in categories" :id="fzeg">
                <p v-if="search == ''">{{ category }}</p>
                <div v-if="search == ''" class="emoji-category-wrapper emoji-categ-content">
                    <span @click="ChooseOne(emojiKey)" v-for="emojiKey in getKeyCategory(category)">
                        {{ enVracs[emojiKey]  }}
                    </span>
                </div>
            </div>
            <h6 v-if="search != ''">Searching emoji ...</h6>
            <div v-if="search != ''" class="emoji-category-wrapper emoji-categ-content">
                
                <span @click="ChooseOne(emojiKey)" v-for="emojiKey in Filtered(search)">
                    {{ enVracs[emojiKey]  }}
                </span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.emoji-wrapper {
    display: block;
    width: 200px;
    height: 300px;
    overflow: hidden;
    position: absolute;
    bottom: 90px;
    /* border: 2px solid #eee; */
    box-shadow: -1px 1px 3px 6px #eee;
    padding: 5px;
    background: white;
}
.emoji-search-input {
    width: 100%;
    position: sticky;
    border-radius: 20px;
    padding-left: 9px;
    display: block !important;
}
.emoji-search-input:focus {
    outline: 0;
}
.emoji-header {

}
.emoji-smeiley-list {
    overflow: scroll;
    height: 300px;
}
.emoji-category-wrapper.emoji-categ-content {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 5px;
}
.emoji-category-wrapper.emoji-categ-content span {
    cursor: pointer;
    display: block;
    font-size: 19px;
}

.emoji-category-wrapper.emoji-categ-content span:hover {
    background-color: #426b68;
    border-radius: 5px;
}
</style>