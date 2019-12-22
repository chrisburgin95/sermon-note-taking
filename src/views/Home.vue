<template>
  <div class="home">
    <div class="view">
      <div class="empty" v-if="sections.length === 0">
        Add a section to get started.
      </div>
      <template v-for="(s, i) in sections">
        <!-- Main Idea -->
        <div class="main-idea" v-if="s.type === 'mainIdea'" :key="i">
          <font-awesome-icon icon="times" @click="remove(i)" />
          <div
            class="input"
            :class="{ placeholder: !s.text }"
            :ref="i"
            contenteditable="true"
            :placeholder="s.placeholder"
            @blur="onInput($event, i)"
            v-html="s.text"
          />
        </div>

        <!-- Point -->
        <div class="point" v-if="s.type === 'point'" :key="i">
          <font-awesome-icon icon="times" @click="remove(i)" />
          <h2
            @blur="onInput($event, i, 'title')"
            contenteditable=""
            placeholder="Add point title."
            v-html="s.title"
            :class="{ placeholder: !s.text }"
          />

          <div
            class="input"
            :class="{ placeholder: !s.text }"
            :ref="i"
            contenteditable="true"
            placeholder="Add point notes"
            @blur="onInput($event, i)"
            v-html="s.notes"
          />
        </div>
      </template>
    </div>
    <div class="controls">
      <button @click="addMainIdea">
        <font-awesome-icon icon="lightbulb" />
      </button>
      <button @click="addPoint">
        <font-awesome-icon icon="sticky-note" />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "home",
  data: () => ({
    sections: []
  }),
  methods: {
    addMainIdea() {
      this.sections.push({
        type: "mainIdea",
        text: "",
        placeholder: "Enter the main idea."
      });
    },
    addPoint() {
      this.sections.push({
        type: "point",
        title: "",
        notes: ""
      });
    },
    remove(id) {
      this.sections = this.sections.filter((_, i) => i !== id);
    },
    onInput(e, id) {
      const type = this.sections[id].type;
      const text = e.target.innerText;

      if (type === "mainIdea") {
        if (!text.trim()) {
          this.remove(id);
        } else {
          this.sections[id].text = text;
        }
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.home {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
}

.view {
  .empty {
    text-align: center;
  }

  > div {
    padding: 24px;
    background: white;
    margin-bottom: 4px;
    position: relative;

    > svg {
      display: none;
      position: absolute;
      top: 0;
      right: 0;
      padding-top: 6px;
      padding-right: 10px;
      font-size: 16px;
      cursor: pointer;
    }

    &:hover {
      svg {
        display: inherit;
      }
    }

    h2 {
      margin: 0;
      font-size: 22px;
      padding: 12px;
    }

    div.input {
      background: white;
      padding: 12px;

      &.placeholder:empty {
        color: rgba(0, 0, 0, 0.5);
      }

      &:focus {
        border: 1px solid rgba(0, 0, 0, 0.4);
        outline: 0;
      }
    }

    &.main-idea {
      .input {
        font-size: 32px;
        font-weight: 600;
      }
    }

    &.point {
      h2 {
        &.placeholder:empty {
          color: rgba(0, 0, 0, 0.5);
        }

        &:focus {
          border: 1px solid rgba(0, 0, 0, 0.4);
          outline: 0;
        }
      }
    }
  }
}

.controls {
  display: flex;
  margin-top: 14px;
  justify-content: flex-end;

  button {
    border: none;
    margin-left: 16px;
    font-size: 32px;
    cursor: pointer;
    background: white;
    width: 75px;
    height: 75px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: 200ms;

    &:hover {
      box-shadow: 1px 1px 8px rgba(0, 0, 0, 0.15);
    }

    svg {
      color: rgba(0, 0, 0, 0.5);
    }
  }
}
</style>
