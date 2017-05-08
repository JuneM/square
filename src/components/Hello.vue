<template>
  <div class="hello">
    <div class="header clearfix">
      <span class="nav">导航</span>
      <span class="remark">备注：展示页面处之改变颜色，不改变数值。改变的数据直接添加到“生成数据列表”中，最终提交数据</span>
    </div>
    <div class="content">
      <div class="item clearfix">
        <label class="float-left">请选择包包类型：</label>
        <div class="type float-left">
          <span v-for="item in type" :class="{active: item.isSelected}" @click="selected(type, item)">{{item.name}}</span>
        </div>
      </div>
      <div class="reference">
        <span><i></i>#e20b0b</span>
        <span><i></i>#e28c0b</span>
        <span><i></i>#0be225</span>
        <span><i></i>#0bbae2</span>
        <span><i></i>#360be2</span>
        <span><i></i>#d50be2</span>
        <span><i></i>#ccf105</span>
      </div>
      <div class="input">
        <div class="flex">
          <label>请输入宽度</label>
          <input type="text" v-model="submitData.content.width">
          <span>(cm)</span>
        </div>
        <div class="flex">
          <label>请输入高度</label>
          <input type="text" v-model="submitData.content.height">
          <span>(cm)</span>
        </div>
        <div class="flex">
          <label>请输入侧边度</label>
          <input type="text" v-model="submitData.content.side">
          <span>(cm)</span>
        </div>
        <div class="flex">
          <label>请输入正面包边颜色</label>
          <input type="text" v-model="submitData.content.fontBorderColor">
        </div>
        <div class="flex">
          <label>请输入底部包边颜色</label>
          <input type="text" v-model="submitData.content.backBorderColor">
        </div>
        <div class="flex">
          <label>请输入侧边包边颜色</label>
          <input type="text" v-model="submitData.content.sideBorderColor">
        </div>
        <div class="confirm">
          <input type="button" value="提交数据" @click="confirm">
        </div>
      </div>
      <div class="image" v-if="!isObjectEmpty(resultData)">
        <div class="img-header clearfix">
          <div class="handler handler-odd float-left" :style="handleOdd">
            <div class="handle-header" :style="handleOddHeader"></div>
            <div class="handle-body">
              <div class="body-R" :style="handleOddBody"></div>
              <div class="body-R" :style="handleOddBody"></div>
            </div>
          </div>
          <div class="handler handler-even float-left" :style="handleEven">
          </div>
          <div class="handler handler-odd float-left" :style="handleOdd">
            <div class="handle-header" :style="handleOddHeader"></div>
              <div class="handle-body">
                <div class="body-R" :style="handleOddBody"></div>
                <div class="body-R" :style="handleOddBody"></div>
              </div>
          </div>
          <div class="handler handler-even float-left" :style="handleEven">
          </div>
        </div>
        <div class="clearfix body">
          <div class="image-num image-1 float-left" :style="imageOne">
            <img>
          </div>
          <div class="image-num image-2 float-left" :style="imageTwo">
            <img>
          </div>
          <div class="image-num image-3 float-left" :style="imageOne">
            <img>
          </div>
          <div class="image-num image-4 float-left" :style="imageTwo">
            <img>
          </div>
        </div>
        <div class="footer">
          <div class="image-num image-5" :style="imageFive">
            <img>
          </div>
        </div>
        
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      type: [{
        name: '类型一',
        attr: 'one',
        isSelected: false
      }, {
        name: '类型二',
        attr: 'two',
        isSelected: false
      }],
      submitData: {
        type: '',
        content: {
          width: 0,
          height: 0,
          side: 0,
          fontBorderColor: '',
          backBorderColor: '',
          sideBorderColor: ''
        }
      },
      imageOne: {},
      imageTwo: {},
      imageFive: {},
      handleOdd: {},
      handleEven: {},
      handleOddHeader: {},
      handleOddBody: {},
      resultData: {}
    }
  },
  methods: {
    isObjectEmpty (obj) {
      let key
      for (key in obj) {
        return false
      }
      return true
    },
    selected (type, item) {
      type.forEach((item) => {
        item.isSelected = false
      })
      item.isSelected = !item.isSelected
      this.submitData.type = item.attr
    },
    confirm () {
      this.resultData = Object.assign({}, this.submitData)
      this.imageOne = {
        width: this.submitData.content.width + 'px',
        height: this.submitData.content.height + 'px',
        backgroundColor: this.submitData.content.fontBorderColor
      }
      this.imageTwo = {
        width: this.submitData.content.side + 'px',
        height: this.submitData.content.height + 'px',
        backgroundColor: this.submitData.content.sideBorderColor
      }
      this.imageFive = {
        width: this.submitData.content.width + 'px',
        height: this.submitData.content.side + 'px',
        backgroundColor: this.submitData.content.backBorderColor
      }
      this.handleOdd = {
        width: parseInt(this.submitData.content.width) + 20 + 'px'
      }
      this.handleEven = {
        width: parseInt(this.submitData.content.side) + 20 + 'px'
      }
      // this.handleOddHeader = {
      //   width: this.submitData.content.width / 4 + 'px'
      // }
      // this.handleOddBody = {
      //   marginLeft: 3 * this.submitData.content.width / 16 + 'px',
      //   marginRight: 3 * this.submitData.content.width / 16 + 'px',
      //   width: this.submitData.content.width / 8 + 'px',
      //   height: this.submitData.content.height / 2 - this.submitData.content.width / 8 + 'px'
      // }
      console.log(this.resultData)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  width: 100%;
  position: relative;
  top: 0;
  background-color: rgba(255, 118, 0, 0.99);
}

.header span {
  float: left;
  text-align: center;
}

.header .nav{
  width: 30%;
  line-height: 56px;
}
.header .remark{
  width: 69%;
  margin: 15px 0;
}
.content {
  margin-top: 30px;
}

.content .item {
  margin-left: 50px;
  padding: 2px 5px;
}

.content .item label{
  width: 156px;
}

.content .item .type {
  cursor: pointer;
}
.content .item .type span{
  margin-right: 50px;
  padding: 3px 5px;
  border: 1px solid transparent;
}

.content .item .type span.active{
  border-color: #00adff;
  color: #00adff
}

.content .item .type span:hover{
  border-color: #00adff;
  color: #00adff
}

.content .input {
  margin-top: 56px;
  margin-left: 50px;
}
.content .reference {
  margin-top: 20px;
  margin-left: 50px;
}

.content .reference span{
  display: inline-block;
  width: 100px;
  height: 20px;
  font-size: 20px;
}
.content .reference span i{
  display: inline-block;
  width: 20px;
  height: 20px;
  margin-right: 5px;
}
.content .reference span:nth-child(1) i{
  background-color: #e20b0b;
}
.content .reference span:nth-child(2) i{
  background-color: #e28c0b;
}
.content .reference span:nth-child(3) i{
  background-color: #0be225;
}
.content .reference span:nth-child(4) i{
  background-color: #0bbae2;
}
.content .reference span:nth-child(5) i{
  background-color: #360be2;
}
.content .reference span:nth-child(6) i{
  background-color: #d50be2;
}
.content .reference span:nth-child(7) i{
  background-color: #ccf105;
}
.content .image {
  margin-left: 50px;
}
.content .image .image-num{
  padding: 10px;
}

.content .image .image-1{
  width: 60px;
  height: 80px;
  background-color: #e20b0b;
}
.content .image .image-2{
  width: 40px;
  height: 80px;
  background-color: #d50be2;
}
.content .image .image-3{
  width: 60px;
  height: 80px;
  background-color: #e20b0b;
}
.content .image .image-4{
  width: 40px;
  height: 80px;
  background-color: #d50be2;
}
.content .image .image-5{
  width: 60px;
  height: 40px;
  background-color: #ccf105;
}

.content .image .handler-odd{
  width: 80px;
  height: 40px;
  margin-top: 40px;
}
.content .image .handler-even{
  width: 60px;
  height: 40px;
}
.content .image .handler-odd .handle-header {
  display: block;  
  height: 0;  
  width: 20px; 
  margin: 0 auto; 
  border-width: 0px 15px 10px 15px;  
  border-style: none solid solid;  
  border-color: transparent transparent #00c8ff;  
}
.content .image .handler-odd .handle-body  {
  margin: 0 auto;
  width: 80px;
}
.content .image .handler-odd .handle-body .body-R{
  display:inline-block;
  margin: 0 14px;
  width: 10px;
  height: 30px;
  background-color: #00c8ff;
}
</style>
