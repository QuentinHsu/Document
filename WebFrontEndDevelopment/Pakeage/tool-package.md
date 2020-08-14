<!-- vscode-markdown-toc -->
* 1. [QRCode 二维码生成](#QRCode)
	* 1.1. [chenfengyuan/vue-qrcode](#chenfengyuanvue-qrcode)
	* 1.2. [vue-qr](#vue-qr)

<!-- vscode-markdown-toc-config
	numbering=true
	autoSave=true
	/vscode-markdown-toc-config -->
<!-- /vscode-markdown-toc -->
# Tool package

##  1. <a name='QRCode'></a>QRCode 二维码生成

###  1.1. <a name='chenfengyuanvue-qrcode'></a>chenfengyuan/vue-qrcode

[npm](https://www.npmjs.com/package/@chenfengyuan/vue-qrcode) | [GitHub](https://github.com/fengyuanchen/vue-qrcode)

**安装**

```
yarn add @chenfengyuan/vue-qrcode vue
```

**配置**

/main.js

```js
import VueQrcode from '@chenfengyuan/vue-qrcode';
Vue.component(VueQrcode.name, VueQrcode);
```

**使用**

```html
<template>
    <div>
        <div>
            <qrcode :value="qrCodeContent" :options="qrCodeOption"></qrcode>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            qrCodeOption: {
                width: 300,
                color: {
                    dark: '#0275d8',
                    light: '#ffffff'
                }
            },
            qrCodeContent: 'VS Code！'
        }
    }
}
```

更加详细的 option 配置说明：[node-qrcode's options](https://github.com/soldair/node-qrcode#qr-code-options)

###  1.2. <a name='vue-qr'></a>vue-qr

更加定制化的二维码生成

[npm](https://www.npmjs.com/package/vue-qr)
