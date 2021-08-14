<template>
  <div id="splash">
    <div id="splash_text"></div>
  </div>
</template>

<script setup>
  import { onMounted } from '@vue/runtime-core';
  import $ from 'jquery';
  import ProgressBar from 'progressbar.js';

  onMounted(() => {
    const bar = new ProgressBar.Line(splash_text, {
      //idを指定
      strokeWidth: 0, //進捗ゲージの太さ
      duration: 1000, //時間指定：単位ms
      trailWidth: 0, //線の太さ
      text: {
        //テキストの形状を直接指定
        style: {
          //天地中央に配置
          position: 'absolute',
          left: '50%',
          top: '50%',
          padding: 0,
          margin: 0,
          transform: 'translate(-50%,-50%)',
          'font-size': '1.2rem',
          color: '#fff',
        },
        autoStyleContainer: false, //自動付与のスタイルを切る
      },
      step(_, bar) {
        bar.setText(Math.round(bar.value() * 100) + ' %'); //ローディングで表示される数値
      },
    });

    bar.animate(1.0, () =>
      //バーを描画する割合を指定．1.0なら100%まで描画
      //アニメーションが終わったら，#splashをフェードアウトさせる
      $('#splash').delay(500).fadeOut(800)
    );
  });
</script>

<style scoped>
  #splash {
    /* fixedで全面に固定 */
    position: fixed;
    z-index: 999;
    width: 100%;
    height: 100%;
    background: #333;
    text-align: center;
    color: #fff;
  }
</style>
