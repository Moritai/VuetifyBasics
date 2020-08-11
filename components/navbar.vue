<template>
<div>
  <!-- ナビゲーションメニューの追加：v-modelのデータプロパティを設定することでナビゲーションメニューの表示非表示を可能にする -->
  <v-navigation-drawer app v-model="drawer" clipped>Navigation Lists</v-navigation-drawer>
  <!-- ナビゲーションメニューの追加　ここまで -->
  <v-app-bar color="primary" dark app clipped-left>
    <!-- ハンバーガーメニューの追加　(クリックすると、drawerの値（true/false）が反転する)-->
    <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
    <!-- ハンバーガーメニューの追加　ここまで -->
     <v-toolbar-title>Vuetify</v-toolbar-title>
     <!-- スペース追加 -->
     <v-spacer></v-spacer>
     <!-- ボタンの追加 -->
     <!-- v-toolbar-items：　　ボタンにマウスオーバーした際にv-app-barコンポーネントの高さ分のクリック領域を持たせる -->
      <v-toolbar-items>
        <v-btn text>For Enterprise</v-btn>
        

        <!-- Supportボタンをクリックするとドロップダウンメニューが現れるように設定 -->
        <v-menu offset-y>
          <template v-slot:activator="{on}">
            <v-btn v-on="on" text>Support<v-icon>mdi-menu-down</v-icon></v-btn>
          </template>
          <!-- v-list：　以下ドロップダウンメニューのリストの設定 -->
          <v-list>
            <!-- サブヘッダーの設定 -->
          　<v-subheader>Get help</v-subheader>
            <!-- ドロップダウンメニューの個々のリスト作成 -->
            <v-list-item v-for="support in supports" :key="support">
            <!--　アイコンの設定  -->
            <v-list-item-icon>
              <v-icon>{{ support.icon }}</v-icon>
            </v-list-item-icon>
            <!-- タイトルの設定 -->
            <v-list-item-content>
              <v-list-item-title>{{ support.name }}</v-list-item-title>
            </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar-items>
  </v-app-bar>
</div>  
</template>
    
<script>
export default {
  name: 'Navbar',
  data(){
    // 初期値をnullにするとデスクトップだとメニューが開き、モバイルだとメニューが閉じた状態で表示される。
    return{
      drawer: null,
      supports:[
        {name: 'Consulting and suppourt',icon: 'mdi-vuetify'},
        {name: 'Discord community',icon: 'mdi-discord'},
        {name: 'Report a bug',icon: 'mdi-bug'},
        {name: 'Github issue board',icon: 'mdi-github-face'},
        {name: 'Stack overview',icon: 'mdi-stack-overflow'},
      ]
    }
  }

}
</script>
    
<style>
     
</style>