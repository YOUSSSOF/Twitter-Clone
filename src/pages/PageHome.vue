<template>
  <q-page class="relative-position">
 
 <q-scroll-area class="absolute fullscreen">

 <div class="q-py-lg q-px-md row items-end
 q-col-gutter-md">
 

<div class="col">
 <q-input 
  class="new-qweet"
  bottom-slots v-model="newQweetContent" 
  placeholder="What `s happening?" 
  counter maxlength="280" 
    autogrow 
  >
        <template v-slot:before>
          <q-avatar size="xl">
            <img src="https://cdn.quasar.dev/img/avatar5.jpg">
          </q-avatar>
        </template>


      
      </q-input>
 
</div>

<div class="col col-shrink">
  <q-btn
          unelevated rounded
          :disable="!newQweetContent" 
          @click="addNewQweet"
          class="q-mb-lg"
          color="primary" 
          label="Qweet" 
           no-caps
        
          />
</div>
 </div>
 
 <q-separator class="divider" size="10px" color="grey-2" />
     






    <q-list  separator>
 
    
    
 
      <q-item
      v-for="qweet in qweets"
      :key="qweet.date"
       class="q-py-md">
       
        <q-item-section avatar top>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar5.jpg">
          </q-avatar>
        </q-item-section>

        <q-item-section class="text-subtitle1">
          <q-item-label >Meisam Ghasemzadeh</q-item-label>
          <span class="text-grey-7">
          09910728389
          </span>
          <q-item-label class="content text-body1">
         {{qweet.content}}
          </q-item-label>

<div class="qwit-icon row justify-between q-mt-sm">
 <q-btn flat round 
 color="grey"
 size="sm"
  icon="far fa-comment" />

   <q-btn flat round 
 color="grey"
 size="sm"
  icon="fas fa-retweet" />

 <q-btn flat round 
 color="grey"
 size="sm"
  icon="far fa-heart" />

 <q-btn flat round 
 @click="deleteQweet(qweet)"
 color="grey"
 size="sm"
  icon="fas fa-trash" />

  

</div>



        </q-item-section>

        <q-item-section side top>
         {{ qweet.date  |  relativeDate}}
        </q-item-section>
      </q-item>

     

    
</q-list>
 </q-scroll-area>













     
  </q-page>
</template>

<script>
import { formatDistance, subDays } from 'date-fns'
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'PageHome',
  data() {
    return {
      newQweetContent: '',
      qweets:[
        {
          content: 'Hi Im Meisam ghasamzadeh , im from iran and i am a student in iran ',
         date:1654452319065
        },
             {
          content: 'im developer ',
         date:1654452356362
        },
      ]
    }
  },
   filters:{
    relativeDate(value){
      return formatDistance(value, new Date())
    }
  },

  
  
  methods:{
    addNewQweet(){
     let NewQweet = {
       content: this.newQweetContent,
       date: Date.now(), 
     }
     
     this.qweets.unshift(NewQweet)
     this.newQweetContent = ''

    },
    deleteQweet(qweet){
      let dataToDelete=qweet.data
      let index=this.qweets.findIndex(qweet=>qweet.data==dataToDelete)
      this.qweets.splice(index,1)
    }
  }
})


</script>

<style lang="sass">
  .new-qweet
    textarea
    font-size:19px
    line-height:1.4 !important

  .divider
   border-top:1px solid
   border-bottom:1px solid
   border:1px solid rgb(220,220,220) 

  .content
white-space:pre-line

.qwit-icon
  margin-left: -5px
</style>
