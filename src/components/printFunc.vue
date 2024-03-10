<template>
  <!-- id 추가-->
  <div id="printMe" >
    <header>
        <h1>안녕하세요, 제 이름은 '하프' 입니다.</h1>
        <h2>어서오세요! 제 소개 페이지에 오신 것을 환영합니다.</h2>
    </header>

    <section>
        <h2>자기 소개</h2>
        <p>안녕하세요! 저는 하프라고 합니다. 개발자로로 활동하고 있습니다. 취미로는 영화보는 문화생활을 즐기고 있습니다. 더 자세한 내용은 아래에서 확인해주세요.</p>
        <div class="contact-icons">
            <a href="mailto:you@example.com" target="_blank"><i class="far fa-envelope"></i></a>
            <a href="tel:+123456789" target="_blank"><i class="fas fa-phone-alt"></i></a>
            <a href="https://github.com/yourusername" target="_blank"><i class="fab fa-github"></i></a>
            <!-- 다른 아이콘 및 링크 추가 가능 -->
        </div>
    </section>

    <section>
        <h2>연락처</h2>
        <p>이메일: [이메일 주소]<br>
        휴대전화: [전화번호]</p>
    </section>

    <footer>
        <p>제작자: 하프 &copy; 2024</p>
    </footer>
  </div>

  <!-- v-print 추가 -->
  <button v-print="'#printMe'" class="print">vue-print-nb</button>
  <button class="print" type="button" @click="printPage">print-js</button>
  <button class="print" type="button" @click="windowPrint">window.print</button>
</template>

<script setup>
import printJS from 'print-js';

const printPage = () => {
  printJS({
    printable: 'printMe',
    type: 'html',
    targetStyles: ['*'],
    maxWidth: '100%',
  });
};

const windowPrint = () => {
  const content = document.querySelector("#printMe").innerHTML;
  const printWindow = window.open('', '_blank', 'width=700, height=600, top=50, left=50, scrollbars=yes');

  printWindow.document.open();
  printWindow.document.write(`
    <html>
    <style>
    body {
      margin: 0;
      padding: 0;
      background-color: #f0f0f0;
      color: #555;
    }

    header {
      background-color: #3498db;
      padding: 30px 0;
      text-align: center;
      color: #fff;
    }

    h1, h2 {
      margin: 0;
    }

    .print {
      cursor: pointer;
      width: 200px;
      height: 50px;
      margin-left: calc(50% - 100px);
      border-radius: 5px;
      border: 1px solid lightgray;
      background-color: #3498db;
      color: white;
      font-weight: bold;
      font-size: 20px;
    }

    section {
        max-width: 800px;
        margin: 30px auto;
        padding: 30px;
        background-color: #fff;
        border-radius: 10px;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
    }

    h2 {
        color: #3498db;
    }

    p {
        line-height: 1.6;
    }

    footer {
        text-align: center;
        padding: 15px;
        background-color: #3498db;
        color: #fff;
        position: fixed;
        bottom: 0;
        width: 100%;
    }

    .contact-icons {
        display: flex;
        justify-content: center;
        margin-top: 20px;
    }

    .contact-icons a {
        color: #555;
        margin: 0 10px;
        font-size: 24px;
        text-decoration: none;
    }

    .contact-icons a:hover {
        color: #3498db;
    }
    </style>
    <head>
      <title>Print</title>
    </head>
    <body>${content}</body>
    </html>`
  );
  printWindow.document.close();
  // 프린트 창이 닫힐 때
  printWindow.onafterprint = () => {
    printWindow.close();
  };
  printWindow.print();
}

</script>

<style scoped>
@import './printFunc.css';

</style>