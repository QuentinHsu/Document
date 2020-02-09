# Element UI

本文档，只记录 Element UI 官方文档中没有提及/介绍，但在使用过程中又发现的。

内容板块划分按照 Element UI 官网文档的板块划分

所以有些板块，可能会有内容，也或许没有。

## 开发指南

## 组件

> Basic

---

> Form

### Upload 上传

在 手动上传 场景下

若用作 “浏览本地文件” 设定类型的 `<el-button>` 不添加如下属性
```
slot="trigger"
```
会导致，该组件内的 **所有** `<el-button>` ，被点击后 **都** “默认 ” 触发打开 “文件选择框”。（以至于“上传”功能按钮，点击后也会打开浏览文件窗口）

所以必须要给是 “浏览本地文件”设定类型的 `<el-button>` ，添加上文所述的 `slot` 属性及属性值 `tirgger`。以免发生不必要的 Bug 。
<details>
 <summary>官方样例代码</summary>

```vue
<el-upload
  class="upload-demo"
  ref="upload"
  action="https://jsonplaceholder.typicode.com/posts/"
  :on-preview="handlePreview"
  :on-remove="handleRemove"
  :file-list="fileList"
  :auto-upload="false">
  <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
  <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传到服务器</el-button>
  <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
</el-upload>
<script>
  export default {
    data() {
      return {
        fileList: [{name: 'food.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}, {name: 'food2.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100'}]
      };
    },
    methods: {
      submitUpload() {
        this.$refs.upload.submit();
      },
      handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePreview(file) {
        console.log(file);
      }
    }
  }
</script>
```
</details>

---