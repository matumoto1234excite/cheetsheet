# Web アニメーション



ろってぃー

lottie を使えばかなり楽



1. `npm i lottie-web`を行う

2. 公式サイトのコミュニティで配布されているアニメーションを json 形式でダウンロードする

3. うにょうにょする

   コンポーネントに新しく`Lottie.vue`としてこれをコピペでいい

   ```vue
   <template>
     <!-- .animationItem(ref="animationContainer") -->
     <div ref="animationContainer" class="animationItem" />
   </template>
   
   <script>
   import lottie from 'lottie-web'
   export default {
     props: {
       options: {
         type: Object,
         required: true
       }
     },
     mounted () {
       const animationEvt = () => {
         lottie.loadAnimation({
           container: this.$refs.animationContainer,
           renderer: 'svg',
           loop: true,
           autoplay: true,
           animationData: this.options.animationData
         })
       }
       const AnimStorage = () => {
         if (sessionStorage.getItem('access')) {
           // 初回アクセス以外の処理
           animationEvt()
         } else {
           // 初回アクセス時の処理
           animationEvt()
           sessionStorage.setItem('access', 0)
         }
       }
       AnimStorage()
     }
   }
   </script>
   
   ```

4. index.vue とか側から呼び出す

   ```vue
   <template>
     <div>
       <article>
         <Lottie :options='lottieOptions' />
       </article>
     </div>
   </template>
   
   <script>
   import Lottie from '~/components/Lottie.vue'
   
   export default {
     components: {
       Lottie
     },
     asyncData () {
       return {
         lottieOptions: {
           animationData: require('~/assets/animation/' + 'hamster.json')
         }
       }
     }
   }
   </script>
   ```

   

これだけで良い







https://photoshopvip.net/121220