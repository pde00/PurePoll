<template lang="jade">
  .dropdown( v-on:click="onClick")
    .dropdownbtn
      .dropdownicon.material-icons {{icon}}
      .name {{name}}
      .arrow.material-icons {{arrow}}
    .dropdowncontent( v-show="visible" )
      .child(v-for = "(aaa, i) in optionIcons", v-on:click="clickchild(i)", v-model="selected")
        .child-icon.material-icons {{aaa['icon']}}
        .child-text {{aaa['text']}}
</template>

<script>
export default {
  name: 'Dropdown',
  props: {
    name: {
      type: String,
      default: ''
    },
    arrow: {
      type: String,
      default: 'keyboard_arrow_down'
    },
    icon: {
      type: String,
      default: ''
    },
    optionIcons: {
      type: Array,
      default() {
        return [{
          icon: 'add',
          text: 'default'
        }];
      }
    }
  },
  data() {
    return {
      visible: false,
      selected: '',
      value: undefined
    };
  },
  methods: {
    onClick() {
      this.visible = !this.visible;
    },
    clickchild(i) {
      this.name = this.optionIcons[i].text;
      this.icon = this.optionIcons[i].icon;
      this.value = this.optionIcons[i].text;
    }
  },
  watch: {
    changeName(i) {
      return this.optionIcons[i].text;
    },
    changeIcon(i) {
      return this.optionIcons[i].icon;
    }
  }
};
</script>

<style scoped lang="sass">
@import "../style/global"
@import "../style/variable"

.rotate-icon
  transform: rotate(180deg)

.dropdown-open
.dropdown
  position: relative
  height: 36px
  .dropdownbtn
    line-height: 36px
    display: flex
    background-color: $sub-color
    color: #fff
    border-radius: 3px
    justify-content: space-between
    @include button-action($sub-color)
    .name
      line-height: 36px
      text-align: center
    .dropdownicon
      color: #fff
      line-height: 36px
      margin: 0 6px
    .arrow
      line-height: 36px
      margin: 0 6px
      transition: all 0.3s ease-in-out

  .dropdowncontent
    z-index: 1
    width: 100%
    position: absolute
    background-color: #ffffff
    top: 40px
    transition: all .3s ease
    @include shadow(.12)
    color: $grey-color
    line-height: 32px
    .child
      display: flex
      .child-icon
        font-size: 32px
      .child-text
        padding-left: 12px
        height: 32px
        line-height: 32px
      &:hover
        background-color: darken(#fff, 20)
</style>
