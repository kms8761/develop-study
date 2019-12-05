# 다음 주소 검색 api

대상: minseok kim
마지막 수정시간: Nov 26, 2019 10:15 AM
만든이: minseok kim
분류: 개발, 문서
진행사항: 검토

# 1.다음 주소 검색 api

## 1. vue에 index.html에 스크립트 추가

    <script src="https://unpkg.com/vue"></script>
        <script src="./daum-post-code.js"></script>
        <script src="http://dmaps.daum.net/map_js_init/postcode.v2.js"></script>

### 1-1 예외 안될경우

Vue CLI 3을 사용하고 있다면, `index.html` 파일이 노출되어 있지 않기 때문에 전역 script를 삽입하기 어려울 수 있습니다.

[html-webpack-externals-plugin](https://www.npmjs.com/package/html-webpack-externals-plugin)을 사용하는 것을 권장합니다.

    npm install --save-dev html-webpack-externals-plugin

## 

vue.cong.js파일에 추가

    const HtmlWebpackExternalsPlugin = require('html-webpack-externals-plugin');
    
    module.exports = {
      configureWebpack: {
        plugins: [
          new HtmlWebpackExternalsPlugin({
            externals: [
              {
                module: 'daum-postcode-api',
                entry: 'http://dmaps.daum.net/map_js_init/postcode.v2.js',
                global: 'daum-postcode-api',
              },
            ],
          }),
        ],
      },
    };

# 2.location.vue 소스 추가

    <template>
    <!-- https://github.com/greenmonn/vue-daum-postcode-example/tree/master/wc 
    참고  -->
      <div>
        <div
          ref="searchWindow"
          :style="searchWindow"
          style="border:1px solid;width:500px;margin:5px 0;position:relative"
        >
          <img
            src="//t1.daumcdn.net/postcode/resource/images/close.png"
            id="btnFoldWrap"
            style="cursor:pointer;position:absolute;right:0px;top:-1px;z-index:1"
            @click="searchWindow.display = 'none'"
            alt="close"
          >
        </div>
        <input type="text" placeholder="우편번호" v-model="postcode">
        <br>
        <input type="button" value="우편번호 찾기" @click="execDaumPostcode">
        <br>
        <input type="text" v-model="address" placeholder="주소">
        <br>
        <input type="text" v-model="extraAddress" ref="extraAddress" placeholder="상세주소">
     
       </div>
      
    </template>
    <script src="http://dmaps.daum.net/map_js_init/postcode.v2.js"></script>
    <script>
    export default {
      data() {
        return {
          searchWindow: {
            display: 'none',
            height: '300px',
          },
          postcode: '',
          address: '',
          extraAddress: '',
        };
      },
      methods: {
        execDaumPostcode() {
          const currentScroll = Math.max(
            document.body.scrollTop,
            document.documentElement.scrollTop,
          );
    
          // eslint-disable-next-line
          new daum.Postcode({
            onComplete: (data) => {
              if (data.userSelectedType === 'R') {
                this.address = data.roadAddress;
              } else {
                this.address = data.jibunAddress;
              }
    
              if (data.userSelectedType === 'R') {
                if (data.bname !== '' && /[동|로|가]$/g.test(data.bname)) {
                  this.extraAddress += data.bname;
                }
    
                if (data.buildingName !== '' && data.apartment === 'Y') {
                  this.extraAddress +=
                    this.extraAddress !== ''
                      ? `, ${data.buildingName}`
                      : data.buildingName;
                }
    
                if (this.extraAddress !== '') {
                  this.extraAddress = ` (${this.extraAddress})`;
                }
              } else {
                this.extraAddress = '';
              }
    
              this.postcode = data.zonecode;
    
              this.$refs.extraAddress.focus();
    
              this.searchWindow.display = 'none';
              document.body.scrollTop = currentScroll;
            },
            onResize: (size) => {
              this.searchWindow.height = `${size.height}px`;
            },
            width: '100%',
            height: '100%',
          }).embed(this.$refs.searchWindow);
    
          this.searchWindow.display = 'block';
        },
      },
    };
    </script>