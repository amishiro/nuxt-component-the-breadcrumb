<template>
  <!-- eslint-disable vue/no-v-html -->
  <nav class="breadcrumb">
    <div
      class="breadcrumb__inner"
      itemscope="itemscope"
      itemtype="http://schema.org/BreadcrumbList"
    >
      <div
        class="breadcrumb__item is-home"
        itemprop="itemListElement"
        itemscope="itemscope"
        itemtype="http://schema.org/ListItem"
      >
        <nuxt-link class="breadcrumb__link" itemprop="item" to="/">
          <span itemprop="name">Home</span>
        </nuxt-link>
        <meta itemprop="position" content="1" />
      </div>
      <div
        v-for="(v, i) in breadcrumb"
        :key="v.url"
        class="breadcrumb__item"
        itemprop="itemListElement"
        itemscope="itemscope"
        itemtype="http://schema.org/ListItem"
      >
        <nuxt-link class="breadcrumb__link" itemprop="item" :to="v.url">
          <span itemprop="name" v-html="v.title" />
        </nuxt-link>
        <meta itemprop="position" :content="i + 2" />
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
    // パンくずナビの配列
    breadcrumb: {
      type: Array,
      default() {
        return [{ title: 'breadcrumbを設定してください。', url: '/' }]
      },
    },
  },
}
</script>

<style lang="scss" scoped>
//-------------------- ベースマージンの設定

// $gap: 8px; //ベースに8pxは計算しやすい
// $gap-s: $gap * 2; //16px
// $gap-m: $gap * 3; //24px
// $gap-l: $gap * 5; //40px
// $gap-xl: $gap * 8; //64px

.breadcrumb {

  // .breadcrumb__inner

  &__inner {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    width: 100%;
    padding: $gap $gap-m;

    // モバイル表示時にはみ出た時に横スクロールをさせる
    overflow: scroll;

    // スクロールバーの削除
    -ms-overflow-style: none; // IE, Edge 対応
    scrollbar-width: none; // Firefox 対応
    &::-webkit-scrollbar {
      display: none; // Chrome, Safari 対応
    }
  }

  // .breadcrumb__item

  &__item {
    display: flex;
    flex: 0 0 auto;
    align-items: center;

    // homeの加工用
    &.is-home {
    }

    // 区切りアイコン
    &:not(:first-child) {
      &::before {
        display: inline;
        padding: 0 $gap/2;
        font-size: 1.1rem;
        content: '/';
      }
    }
  }

  // .breadcrumb__link

  &__link {
    padding: 0 $gap/2;
    font-size: 1.1rem;
    font-weight: bold;
    text-decoration: none;
    &:hover {
      text-decoration: underline;
    }
  }
}
</style>
