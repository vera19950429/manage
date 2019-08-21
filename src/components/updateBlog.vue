<template>
  <div>
    <el-form
      ref="form"
      label-width="80px"
    >
      <el-form-item label="id">
        <el-input
          v-model="id"
          disabled
        ></el-input>
      </el-form-item>
      <el-form-item label="上传贴图文件">
        <el-input v-model="photoPath" disabled>{{this.photoPath}}</el-input>
        <el-upload
          class="upload-demo"
          ref="uploadphoto"
          name="file"
          :action="photoPathUrl()"
          :file-list="fileList"
          :auto-upload="false"
        >
          <el-button
            slot="trigger"
            size="small"
            type="primary"
          >选取文件</el-button>
          <el-button
            style="margin-left: 10px;"
            size="small"
            type="success"
            @click="submitUploadphoto"
          >上传到服务器</el-button>
          <div
            slot="tip"
            class="el-upload__tip"
          >只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-form-item>
      <el-form-item label="上传背景文件">
        <el-input v-model="backPath" disabled>{{this.backPath}}</el-input>
        <el-upload
          class="upload-demo"
          ref="uploadback"
          name="file"
          :action="backPathUrl()"
          :file-list="fileList"
          :auto-upload="false"
        >
          <el-button
            slot="trigger"
            size="small"
            type="primary"
          >选取文件</el-button>
          <el-button
            style="margin-left: 10px;"
            size="small"
            type="success"
            @click="submitUploadback"
          >上传到服务器</el-button>
          <div
            slot="tip"
            class="el-upload__tip"
          >只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-form-item>
      <el-form-item label="上传模型文件">
        <el-input v-model="modelPath" disabled>{{this.modelPath}}</el-input>
        <el-upload
          class="upload-demo"
          ref="uploadmodel"
          name="file"
          :action="modelPathUrl()"
          :file-list="fileList"
          :auto-upload="false"
        >
          <el-button
            slot="trigger"
            size="small"
            type="primary"
          >选取文件</el-button>
          <el-button
            style="margin-left: 10px;"
            size="small"
            type="success"
            @click="submitUploadmodel"
          >上传到服务器</el-button>
          <div
            slot="tip"
            class="el-upload__tip"
          >只能上传jpg/png文件，且不超过500kb</div>
        </el-upload>
      </el-form-item>
      <el-form-item>
        <el-button
          type="primary"
          @click="updateBlog"
        >立即修改</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      id: "",
      modelPath: "",
      photoPath: "",
      backPath: "",
      createTime: "",
      params: ""
    };
  },
  created() {
    this.axios.get("api/uploads/search/" + this.$route.params.id).then(result => {
      // 注意： 通过 $http 获取到的数据，都在 result.body 中放着

      if (result.status === 200) {
        // 成功了
        var result = result.data;
        this.id = result.id;
        this.modelPath = result.modelPath;
        this.photoPath = result.photoPath;
        this.backPath = result.backPath;
        this.params = result.params;
      } else {
        // 失败了
        alert("获取数据失败！");
      }
    });
  },
  methods: {
    modelPathUrl() {
      return "api/uploads/" + this.id + "/model_path";
    },
    photoPathUrl() {
      return "api/uploads/" + this.id + "/photo_path";
    },
    backPathUrl() {
      return "api/uploads/" + this.id + "/back_path";
    },
    submitUploadphoto() {
      this.$refs.uploadphoto.submit();
    },
    submitUploadback() {
      this.$refs.uploadback.submit();
    },
    submitUploadmodel() {
      this.$refs.uploadmodel.submit();
    },
    updateBlog() {
      this.$http
        .put("updateBlog", {
          id: this.id,
          title: this.title,
          link: this.link,
          author: this.author,
          tag: this.tag
        })
        .then(result => {
          var result = result.body;
          if (result.code === 200) {
            alert("修改成功！");
          } else {
            // 失败了
            alert("修改失败！");
          }
        });
    }
  }
};
</script>
