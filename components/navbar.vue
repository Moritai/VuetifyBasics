<template>
<div>
  <!-- ナビゲーションメニューの追加：v-modelのデータプロパティを設定することでナビゲーションメニューの表示非表示を可能にする -->
  <v-navigation-drawer app v-model="drawer" clipped>
    <!-- ナビゲーションメニューの中身の定義 -->
    <v-container>
      <!-- ナビゲーションメニューの項目の一つ（タイトル）を定義 -->
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title grey--text text--darken-2">
            Navigation lists
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <!--　分かれ目のための線を描写  -->
      <v-divider></v-divider>

      <!--　ナビゲーションメニューの項目をdataのnav_listsを元に順々に作成していく  -->
      <!-- v-listにnavとdenseを設定しているが、どちらもスタイリングを調整するために使っている -->
      <v-list nav dense>
        <!-- no-actionを設定しなければ下の階層の左側のpaddingが設定されない
         :append-iconを設定しなければ下の階層がないメニューについても右側に矢印が表示される
         :append-icon=”””(ダブルクオテーション、シングル、シングル、ダブル)にすれば矢印が表示されない。
         -->
        <v-list-group 
        v-for="nav_list in nav_lists" 
        :key="nav_list.name" 
        :prepend-icon="nav_list.icon" 
        no-action 
        :append-icon="nav_list.lists ? undefined : ''"> 
          <template v-slot:activator>
            <v-list-item-content>
              <v-list-item-title>{{ nav_list.name }}</v-list-item-title>
            </v-list-item-content>
          </template>
          <v-list-item v-for="list in nav_list.lists" :key="list">
            <v-list-item-content>
              <v-list-item-title>{{ list }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-group>
      </v-list>

    </v-container>
  </v-navigation-drawer>
  <!-- ナビゲーションメニューの追加　ここまで -->

  <v-app-bar color="primary" dark app clipped-left>
    <!-- ハンバーガーメニューの追加　(クリックすると、drawerの値（true/false）が反転する)-->
    <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
    <!-- ハンバーガーメニューの追加　ここまで -->

     <!-- <v-toolbar-title to="/enterprise">Vuetify</v-toolbar-title> -->
     <nuxt-link to="/">
      <v-toolbar-title class="white--text text--darken-2" v-if="$vuetify.breakpoint.mdOnly">
        Vuetify
      </v-toolbar-title>
    </nuxt-link>


     <!-- スペース追加 -->
     <v-spacer></v-spacer>
     <!-- ボタンの追加 -->
     <!-- v-toolbar-items：　　ボタンにマウスオーバーした際にv-app-barコンポーネントの高さ分のクリック領域を持たせる -->
      <v-toolbar-items>
        <v-btn text to="/enterprise">For Enterprise</v-btn>
        

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
            <v-list-item v-for="support in supports" :key="support.id" :to="support.link">
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
        {
          id: 1,
          name: 'Consulting and suppourt',
          icon: 'mdi-vuetify',
          link:'/consulting-and-support'
        },
        {
          id: 2,
          name: 'Discord community',
          icon: 'mdi-discord',
          link:'/discord-community'},
        {
          id: 3,
          name: 'Report a bug',
          icon: 'mdi-bug',
          link:'/report-a-bug'
        },
        {
          id: 4,
          name: 'Github issue board',
          icon: 'mdi-github-face',
          link:'/guthub-issue-board'
        },
        {
          id: 5,
          name: 'Stack overview',
          icon: 'mdi-stack-overflow',
          link:'/stack-overview'
        },
      ],

      nav_lists:[
        {
          name: 'Getting Started',
          icon: 'mdi-speedometer',
          lists:['Quick Start','Pre-made layouts']
        },
        {
          name: 'Customization',
          icon: 'mdi-cogs' 
        },
        {
          name: 'Styles & animations',
          icon: 'mdi-palette',
          lists:['Colors','Content','Display']
        },
        {
          name: 'UI Components',
          icon: 'mdi-view-dashboard',
          lists:['API explorer','Alerts']
        },
        {
          name: 'Directives',
          icon: 'mdi-function'
        },
        {
          name: 'Preminum themes',
          icon: 'mdi-vuetify'
        },
        // {name: 'Getting Started',icon: 'mdi-vuetify'},
        // {name: 'Customization',icon: 'mdi-cogs'},
        // {name: 'Styles & animations',icon: 'mdi-palette'},
        // {name: 'UI Components',icon: 'mdi-view-dashboard'},
        // {name: 'Directives',icon: 'mdi-function'},
        // {name: 'Preminum themes',icon: 'mdi-vuetify'},
      ]
    }
  }

}
</script>
    
<style>
     
</style>