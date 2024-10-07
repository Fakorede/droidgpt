<template>
  <main class="flex w-full h-full">
    <div class="w-full h-full flex flex-col justify-between">

      <div class="content-container flex justify-between w-full h-full" class:open>

        <div class="sidebar-container w-0 h-full">
          <!-- sidebar... -->
        </div>

        <div class="chat-container w-full" :class="loading">
          <deep-chat
            :avatars="false"
            :introMessage="message"
            :directConnection="directConnection"
            style="border-radius: 4px; width: 100vw ;height: 100vh; padding-top: 0px"
            :textInput='{
              "disabled": false,
              "styles": {
                "text": {"color": "black"},
                "container": {"maxHeight": "50px", "backgroundColor": "#f5f9ff"},
                "focus": {"border": "2px solid #502e81"}
              },
              "placeholder": {"text": "Ask me anything related to Android Development", "style": {"color": "#502e81"}},
              // "characterLimit": 10,
            }'
            auxiliaryStyle="
              ::-webkit-scrollbar {
                width: 10px;
                height: 10px;
              }
              ::-webkit-scrollbar-thumb {
                background-color: #502e81;
                border-radius: 5px;
              }"
            :messageStyles='{
              "default": {
                "shared": {"innerContainer": {"fontSize": "1rem"}},
                "ai": {"bubble": {"backgroundColor": "#feca35"}},
                "user": {"bubble": {"backgroundColor": "#502e81"}},
              }
            }'
            :chatStyle='{
              "display": "block",
              "width": "100%",
              "height": "100%",
              "backgroundColor": "#fff",
              // "border": "none",
              "fontSize": "17px",
              "fontFamily": ""
            }'
            :inputAreaStyle='{"fontSize": "1rem"}'
            :connect='{"stream": true}'
          ></deep-chat>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
// "'system-ui, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'"
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'
import 'deep-chat';

export default {
  name: 'App',
  data() {
    return {
      loading: false,
      history: [
        { role: 'user', text: 'Hey, how are you today?' },
        { role: 'ai', text: 'I am doing very well!' },
      ],
      message: {
        "text": "Hi, I am DroidGPT. Ask me anything about Android Development!"
      },
      directConnection: {
        "openAI": {
          "key": import.meta.env.VITE_OPENAI_API_KEY,
          "assistant": {
            "assistant_id": import.meta.env.VITE_OPENAI_ASSISTANT_ID,
          },
          "chat": {
            "system_prompt": "You are a helpful assistant", 
            "model": "gpt-4o",
            "temperature": 0.2,
            "top_p": 0.1,
            // max_tokens: 2000
          },
        }
      }
    };
  },
};
</script>

<style scoped>
main {
  font-family: system-ui, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  width: 100%;
  height: calc(100% + env(safe-area-inset-top));
  padding-top: env(safe-area-inset-top);
}

.content-container {
  height: calc(100% - 3rem);
  width: 100%;
  padding: 0 env(safe-area-inset-right) env(safe-area-inset-bottom) env(safe-area-inset-left);
}

.loading {
  filter: blur(2px);
  pointer-events: none;
}

.chat-container {
  transition: width 0.3s ease;
}
.sidebar-container {
  transition: width 0.3s ease;
}

.open > .sidebar-container {
  width: 300px;
}

.open > .chat-container {
  width: calc(100% - 300px);
}

@media only screen and (max-width: 700px) {
  .open > .sidebar-container {
    width: 0;
  }

  .open > .chat-container {
    width: 100%;
  }
}
/* div {
  font-family: sans-serif;
  text-align: center;
  justify-content: center;
  display: grid;
} */

/* header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} */
</style>
