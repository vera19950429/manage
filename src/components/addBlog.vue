<template>
  <div>
    <el-form
      ref="form"
      label-width="80px"
    >
      <el-form-item label="标题">
        <el-input v-model="id"></el-input>
        <el-button @click="newId()">新建</el-button>
      </el-form-item>
      <el-form-item label="上传贴图文件">
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
  methods: {
    newId() {
      this.axios.post("api/uploads/new/" + this.id)
        .then(result => {
          alert("创建成功");
        })
    },
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

  }
};
</script>
