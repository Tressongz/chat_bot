<template>
  <div class="component">
    <div class="interface">
      <div id="messages" class="messages">
        <transition-group name="message">
          <li
              v-bind:class="{bot: message.author === 'bot', user: message.author === 'user'}"
              :key="message.id"
              class="message"
              v-for="message in messages"
          >
            {{ message.message }}
          </li>
        </transition-group>
      </div>

      <div class="buttons">
        <div
            v-if="btnState === 'main'"
            @click="sendMessage(button)"
            class="button"
            v-for="button in buttons"
            :key="button.id"
        ><hr>
          {{ button.data }}
        </div>

        <div
            v-if="btnState === 'pizza'"
            class="button"
            @click="sendMessage(button)"
            v-for="button in buttonsPizza"
            :key="button.id"
        ><hr>
          {{ button.data }}
        </div>

        <div
            v-if="btnState === 'alarm'"
            class="button"
            @click="sendMessage(button)"
            v-for="button in buttonsAlarm"
            :key="button.id"
        ><hr>
          {{ button.data }}
        </div>

        <div
            v-if="btnState === 'weather'"
            class="button"
            @click="sendMessage(button)"
            v-for="button in buttonsWeather"
            :key="button.id"
        ><hr>
          {{ button.data }}
        </div>


      </div>

    </div>


  </div>
</template>

<script>
export default {
  data() {
    return {
      id: 0,
      messages: [
        {id: 1, author: 'bot', message: 'Приветствую тебя, гость!'}
      ],
      buttons: [
        {id: 1, type: 'pizza', data: 'Заказать пиццу'},
        {id: 2, type: 'alarm', data: 'Завести будильник'},
        {id: 3, type: 'weather', data: 'Узнать погоду'}
      ],
      buttonsPizza: [
        {id: 1, type: 'peperoni', data: 'Пицца "Пеперони"'},
        {id: 2, type: 'margarita', data: 'Пицца "Маргарита"'},
        {id: 3, type: 'cheese', data: 'Пицца "4 сыра"'},
        {id: 4, type: 'main', data: 'В главное меню'}
      ],
      buttonsAlarm: [
        {id: 1, type: 'morning', data: 'Завести на 7 утра'},
        {id: 2, type: 'after-morning', data: 'Завести на 9 утра'},
        {id: 3, type: 'dinner', data: 'Завести на 11 утра'},
        {id: 4, type: 'main', data: 'В главное меню'}
      ],
      buttonsWeather: [
        {id: 1, type: 'now', data: 'Погода на сегодня'},
        {id: 2, type: 'yesterday', data: 'Погода на завтра'},
        {id: 3, type: 'after', data: 'Погода на послезавтра'},
        {id: 4, type: 'main', data: 'В главное меню'}
      ],
      lastMsg: 'bot',
      btnState: 'main',
      down: null
    }
  },
  methods: {
    sendMessage(button) {
      this.id = this.id + 1
      let object = {id: this.id, author: 'user', message: ''}
      if (button.type === 'pizza') {
        object.message = 'Хочу заказать пиццу'
        this.messages.push(object)
        this.btnState = 'pizza'
      } else if (button.type === 'alarm') {
        object.message = 'Хочу завести будильник'
        this.messages.push(object)
        this.btnState = 'alarm'
      } else if (button.type === 'weather') {
        object.message = 'Хочу узнать погоду'
        this.messages.push(object)
        this.btnState = 'weather'
      }
      // Pizza module
      else if (button.type === 'peperoni') {
        object.message = 'Закажи пиццу "Пеперони"'
        this.messages.push(object)
        this.btnState = 'main'
      }
      else if (button.type === 'margarita') {
        object.message = 'Закажи пиццу "Маргарита"'
        this.messages.push(object)
        this.btnState = 'main'
      }
      else if (button.type === 'cheese') {
        object.message = 'Закажи пиццу "4 сыра"'
        this.messages.push(object)
        this.btnState = 'main'
      }
      // Alarm module
      else if (button.type === 'morning') {
        object.message = 'Заведи будильник на 7 часов утра'
        this.messages.push(object)
        this.btnState = 'main'
      }
      else if (button.type === 'after-morning') {
        object.message = 'Заведи будильник на 9 часов утра'
        this.messages.push(object)
        this.btnState = 'main'
      }
      else if (button.type === 'dinner') {
        object.message = 'Заведи будильник на 11 часов утра'
        this.messages.push(object)
        this.btnState = 'main'
      }
      // Weather module
      else if (button.type === 'now') {
        object.message = 'Покажи погоду на сегодня'
        this.messages.push(object)
        this.btnState = 'main'
      }
      else if (button.type === 'yesterday') {
        object.message = 'Покажи погоду на завтра'
        this.messages.push(object)
        this.btnState = 'main'
      }
      else if (button.type === 'after') {
        object.message = 'Покажи погоду на послезавтра'
        this.messages.push(object)
        this.btnState = 'main'
      }
      // Return module
      else if (button.type === 'main') {
        object.message = 'Вернуться в главное меню'
        this.messages.push(object)
        this.btnState = 'main'
      }
      setTimeout(() => {
        this.down.scrollTop = this.down.scrollHeight
      })
      this.lastMsg = 'user'
    }
  },
  mounted() {
    this.id = this.messages.length
    this.down = document.getElementById('messages')
  },
  watch: {
    lastMsg() {
      if (this.lastMsg === 'user') {
        this.id = this.id + 1
        let object = {id: this.id, author: 'bot', message: ''}

        setTimeout(() => {
          if (this.messages[this.messages.length - 1].message === 'Хочу заказать пиццу') {
            object.message = 'Какую пиццу хотите заказать?'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Хочу завести будильник') {
            object.message = 'На какое время установить будильник?'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Хочу узнать погоду') {
            object.message = 'На какой день хотите узнать погоду?'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Закажи пиццу "Пеперони"') {
            object.message = 'Заказал Вам пиццу "Пеперони"'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Закажи пиццу "Маргарита"') {
            object.message = 'Заказал Вам пиццу "Маргарита"'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Закажи пиццу "4 сыра"') {
            object.message = 'Заказал Вам пиццу "4 сыра"'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Заведи будильник на 7 часов утра') {
            object.message = 'Завёл будильник на 7 часов утра'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Заведи будильник на 9 часов утра') {
            object.message = 'Завёл будильник на 9 часов утра'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Заведи будильник на 11 часов утра') {
            object.message = 'Завёл будильник на 11 часов утра'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Покажи погоду на сегодня') {
            object.message = 'Сегодня солнечно, 25 градусов тепла'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Покажи погоду на завтра') {
            object.message = 'Завтра облачно, 20 градусов тепла'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Покажи погоду на послезавтра') {
            object.message = 'Послезавтра дожди, 19 градусов тепла'
            this.messages.push(object)
          } else if (this.messages[this.messages.length - 1].message === 'Вернуться в главное меню') {
            object.message = 'Возвращаю в главное меню..'
            this.messages.push(object)
          } else {
            object.message = 'Не понимаю Вашего запроса'
            this.messages.push(object)
          }
          setTimeout(()=> {
            this.down.scrollTop = this.down.scrollHeight
          }, 500)
          this.lastMsg = 'bot'
        }, 1000)
      }
    }
  }
}
</script>


<style lang="sass" scoped>
.component
  display: flex
  align-items: center
  justify-content: center
  flex-direction: column

.interface
  display: flex
  flex-direction: column
  background-color: #73bae1
  border-radius: 15px
  width: 400px
  height: 500px
  box-shadow: 0 4px 2px 1px
  padding: 15px 15px 0 15px

.messages
  overflow-y: scroll
  white-space: nowrap
  display: flex
  flex-direction: column
  width: 100%

.message
  margin-right: 10px
  display: flex
  border-radius: 15px
  padding: 8px
  margin-bottom: 10px
  box-shadow: 0 2px 1px 2px #51b3e8

.bot
  background-color: #1fe7ce
  align-self: flex-start

.user
  background-color: #48ee5f
  align-self: flex-end

.buttons
  margin-top: auto
  display: flex
  justify-content: space-around

.button
  padding: 5px
  background-color: #73bae1
  border-radius: 10px
  cursor: pointer
  transition: .5s

.button:hover
  background-color: #48ee5f
  opacity: 0.9


.message-enter-active,
.message-leave-active
  transition: all .5s ease

.message-enter-from,
.message-leave-to
  opacity: 0
  transform: translateY(130px)

.message-move
  transition: transform 0.6s ease



html
  scrollbar-width: thin
  scrollbar-color: blue orange

*::-webkit-scrollbar,
html *::-webkit-scrollbar
  height: 12px
  width: 12px

*::-webkit-scrollbar-track,
html *::-webkit-scrollbar-track
  background: #73bae1

*::-webkit-scrollbar-thumb,
html *::-webkit-scrollbar-thumb
  background-color: rgba(213, 229, 239, 0.27)
  border-radius: 5px
  border: 3px solid #73bae1

@media (min-width: 400px) and (max-width: 560px)
  .buttons
    flex-direction: column
  .interface
    width: 100%
  .user
    align-self: flex-start

@media (min-width: 150px) and (max-width: 400px)
  .buttons
    flex-direction: column
  .interface
    width: 100%
  .user
    align-self: flex-start
  *
    font-size: 10px

</style>
