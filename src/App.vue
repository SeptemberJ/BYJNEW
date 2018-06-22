<template>
<div class="com-app">
    <transition>
        <router-view class="child-view"></router-view>
    </transition>
</div>
</template>
<script>
import Vue from 'vue'
import axios from 'axios'
import $ from 'jquery'

  export default{
    data: function () {
      return {
      }
    },
    
    created: function () {
    	var sha1;
		(function (sha1) {
		    var POW_2_24 = Math.pow(2, 24);
		    var POW_2_32 = Math.pow(2, 32);

		    function hex(n) {
		        var s = "",
		            v;
		        for (var i = 7; i >= 0; --i) {
		            v = (n >>> (i << 2)) & 15;
		            s += v.toString(16);
		        }
		        return s;
		    }

		    function lrot(n, bits) {
		        return ((n << bits) | (n >>> (32 - bits)));
		    }
		    var Uint32ArrayBigEndian = (function () {
		        function Uint32ArrayBigEndian(length) {
		            this.bytes = new Uint8Array(length << 2);
		        }
		        Uint32ArrayBigEndian.prototype.get = function (index) {
		            index <<= 2;
		            return (this.bytes[index] * POW_2_24) + ((this.bytes[index + 1] << 16) | (this.bytes[index + 2] << 8) | this.bytes[index + 3]);
		        };
		        Uint32ArrayBigEndian.prototype.set = function (index, value) {
		            var high = Math.floor(value / POW_2_24),
		                rest = value - (high * POW_2_24);
		            index <<= 2;
		            this.bytes[index] = high;
		            this.bytes[index + 1] = rest >> 16;
		            this.bytes[index + 2] = (rest >> 8) & 255;
		            this.bytes[index + 3] = rest & 255;
		        };
		        return Uint32ArrayBigEndian;
		    })();

		    function string2ArrayBuffer(s) {
		        s = s.replace(/[\u0080-\u07ff]/g, function (c) {
		            var code = c.charCodeAt(0);
		            return String.fromCharCode(192 | code >> 6, 128 | code & 63);
		        });
		        s = s.replace(/[\u0080-\uffff]/g, function (c) {
		            var code = c.charCodeAt(0);
		            return String.fromCharCode(224 | code >> 12, 128 | code >> 6 & 63, 128 | code & 63);
		        });
		        var n = s.length,
		            array = new Uint8Array(n);
		        for (var i = 0; i < n; ++i) {
		            array[i] = s.charCodeAt(i);
		        }
		        return array.buffer;
		    }

		    function hash(bufferOrString) {
		        var source;
		        if (bufferOrString instanceof ArrayBuffer) {
		            source = bufferOrString;
		        } else {
		            source = string2ArrayBuffer(String(bufferOrString));
		        }
		        var h0 = 1732584193,
		            h1 = 4023233417,
		            h2 = 2562383102,
		            h3 = 271733878,
		            h4 = 3285377520,
		            i, sbytes = source.byteLength,
		            sbits = sbytes << 3,
		            minbits = sbits + 65,
		            bits = Math.ceil(minbits / 512) << 9,
		            bytes = bits >>> 3,
		            slen = bytes >>> 2,
		            s = new Uint32ArrayBigEndian(slen),
		            s8 = s.bytes,
		            j, w = new Uint32Array(80),
		            sourceArray = new Uint8Array(source);
		        for (i = 0; i < sbytes; ++i) {
		            s8[i] = sourceArray[i];
		        }
		        s8[sbytes] = 128;
		        s.set(slen - 2, Math.floor(sbits / POW_2_32));
		        s.set(slen - 1, sbits & 4294967295);
		        for (i = 0; i < slen; i += 16) {
		            for (j = 0; j < 16; ++j) {
		                w[j] = s.get(i + j);
		            }
		            for (; j < 80; ++j) {
		                w[j] = lrot(w[j - 3] ^ w[j - 8] ^ w[j - 14] ^ w[j - 16], 1);
		            }
		            var a = h0,
		                b = h1,
		                c = h2,
		                d = h3,
		                e = h4,
		                f, k, temp;
		            for (j = 0; j < 80; ++j) {
		                if (j < 20) {
		                    f = (b & c) | ((~b) & d);
		                    k = 1518500249;
		                } else {
		                    if (j < 40) {
		                        f = b ^ c ^ d;
		                        k = 1859775393;
		                    } else {
		                        if (j < 60) {
		                            f = (b & c) ^ (b & d) ^ (c & d);
		                            k = 2400959708;
		                        } else {
		                            f = b ^ c ^ d;
		                            k = 3395469782;
		                        }
		                    }
		                }
		                temp = (lrot(a, 5) + f + e + k + w[j]) & 4294967295;
		                e = d;
		                d = c;
		                c = lrot(b, 30);
		                b = a;
		                a = temp;
		            }
		            h0 = (h0 + a) & 4294967295;
		            h1 = (h1 + b) & 4294967295;
		            h2 = (h2 + c) & 4294967295;
		            h3 = (h3 + d) & 4294967295;
		            h4 = (h4 + e) & 4294967295;
		        }
		        return hex(h0) + hex(h1) + hex(h2) + hex(h3) + hex(h4);
		    }
		    sha1.hash = hash;
		})(sha1 || (sha1 = {}));

		var companyId = '72c0319a64294769ae87c091f3c37737';//'a59e68f2d99744019f38d6864b55fc84';
		var urlCode = 'ZHCS';
		var appid = 'wx99fde7318286d01a';//'wx99fde7318286d01a';
		var appsecret = '5fdd24904f050ba0dd58f57de054e1fe'//'d79c50de6a88c2b6386877ffb981a81f';
		var mytimestamp = (Date.parse(new Date())) / 1000;
		var mynonceStr = sha1.hash(String(mytimestamp)).substring(0, 16);
		var mywxjsapi_ticket = '';
		var mysignature = '';

		function GetJsapiTicket(){
			alert('GetJsapiTicket')
			axios.post('https://m2c.mindmedia.cn/wxm/auth/getJsApiAccessToken/' + companyId + '.do',
			).then((res)=> {
				console.log('jsapi_ticket---')
				console.log(res.data.infoData)
				var mysignatureReall = "jsapi_ticket=" + res.data.infoData + "&noncestr=" + mynonceStr + "&timestamp=" + mytimestamp + "&url=" + window.location.href.split("#")[0];
		    	mysignature = sha1.hash(mysignatureReall)
		    	console.log('mysignature---')
		    	console.log(mysignature)
		    	wx.config({  
				    debug: true, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。  
				    appId: appid, // 必填，公众号的唯一标识  
				    timestamp: mytimestamp, // 必填，生成签名的时间戳  
				    nonceStr: mynonceStr, // 必填，生成签名的随机串  
				    signature:sha1.hash(mysignatureReall),// 必填，签名，见附录1  
				    jsApiList: [  
				        'checkJsApi',  
				        'onMenuShareTimeline',  
				        'onMenuShareAppMessage',  
				        'onMenuShareQQ',  
				        'onMenuShareWeibo',  
				        'chooseWXPay'  
				    ] // 必填，需要使用的JS接口列表，所有JS接口列表见附录2  
				});
				wx.error(function (res) {
					console.log('config error---');
					alert('config error---' + res)
		            console.log(res);
		        });
		        wx.ready(function () {  
				    wx.onMenuShareTimeline({  
				        title: '100000瓶粱大侠毕业用酒免费申领中……', // 分享标题  
				        link: 'wxmms.swissems.cn', // 分享链接,将当前登录用户转为puid,以便于发展下线  
				        imgUrl: 'https://wxmms.swissems.cn/byj/shareTitImg.jpg', // 分享图标  
				        success: function () {   
				            // 用户确认分享后执行的回调函数  
				            console.log('分享成功');  
				        },  
				        cancel: function () {   
				            // 用户取消分享后执行的回调函数  
				        }  
				    });  
				}); 
				
			}).catch((error)=> {
				console.log(error)
			})
		}


		GetJsapiTicket()
      
    },
    computed: {
      activeRoute(){
        return this.$store.state.activeRoute
       }
      
    },
    watch: {
      
    },
    components: {
      
      

    },
    methods: {
     

    }
  }
</script>
<style scoped>

</style>
