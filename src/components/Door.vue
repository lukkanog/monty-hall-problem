<template>
  <div class="door-area">
      <div class="door-frame" :class="{selected: isSelected && !isOpen}">
          <gift v-if="hasGift && isOpen"/>
      </div>
      <div 
        class="door" 
        @click="isSelected = !isSelected"
        :class="{open: isOpen}"
      >
          <p class="number" :class="{selected: isSelected}">{{ number }} </p>
          <div 
            class="knob" 
            :class="{selected: isSelected}"
            @click.stop="isOpen = !isOpen"
          >
          </div>
      </div>
  </div>
</template>

<script>
import Gift from "@/components/Gift.vue"

export default {
    name: 'Door',
    components: {
        Gift
    },
    props: {
        number: {
            type: String,
            required: true
        },
        hasGift: {
            type: Boolean,
            required: true
        },
    },
    data: () => ({
        isOpen: false,
        isSelected: false,
    })
}
</script>

<style>

.door-area {
    position: relative;
    width: 200px;
    height: 310px;
    border-bottom: 10px solid #AAA;
    margin-bottom: 20px;
    font-size: 3rem;
    display: flex;
    justify-content: center;
    transition: .2s ease-in-out;
}

.door-frame {
    position: absolute;
    height: 300px;
    width: 180px;
    border: 5px solid #a52a2a;
    border-bottom: none;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    transition: inherit;
}

.door-frame.selected {
    border: 5px solid #ffff00;
    border-bottom: none;
}

.door {
    position: absolute;
    top: 5px;
    height: 295px;
    width: 170px;
    background-color: #b34f08;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    transition: inherit;
}

.door.open {
    background-color: #42424277;
}

.open .knob,
.open .number {
    display: none;
}

.number {
    transition: inherit;
    user-select: none;
}

.number.selected {
    color: #ffff00;
}

.knob {
    height: 20px;
    width: 20px;
    border-radius: 50%;
    background-color: #a52a2a;
    align-self: flex-start;
    margin-top: 60px;
    cursor: pointer;
}

.knob.selected{
    background-color: #ffff00;
}
</style>