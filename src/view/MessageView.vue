<template>
  <div class="message-container">
    <el-row>
      <el-col :span="24">
        <el-card>
          <el-tabs class="tabs" v-model="current">
            <!-- 未读消息 -->
            <el-tab-pane :label="'Step1:填写投票基本消息'" name="first">
              <el-form :model="form" >
                <el-form-item label="活动名称">
                  <el-input v-model="form.name" />
                </el-form-item>
                <el-form-item label="活动区域">
                  <el-select v-model="form.region" placeholder="请选择你的区域">
                    <el-option label="上海" value="上海" />
                    <el-option label="北京" value="北京" />
                    <el-option label="西安" value="西安" />
                    <el-option label="杭州" value="杭州" />
                  </el-select>
                </el-form-item>
              </el-form>
              <el-form-item label="活动时间">
                <el-date-picker
                    v-model="value2"
                    type="datetimerange"
                    :shortcuts="shortcuts"
                    range-separator="To"
                    start-placeholder="Start date"
                    end-placeholder="End date"
                />

              </el-form-item>
              <el-form-item label="Instant delivery">
                <el-switch v-model="form.delivery" />
              </el-form-item>
              <el-form-item label="活动类型">
                <el-checkbox-group v-model="form.type">
                  <el-checkbox label="公开场景" name="type" />
                  <el-checkbox label="特定场景" name="type" />
<!--                  <el-checkbox label="Offline activities" name="type" />-->
<!--                  <el-checkbox label="Simple brand exposure" name="type" />-->
                </el-checkbox-group>
              </el-form-item>
<!--              <el-form-item label="Resources">-->
<!--                <el-radio-group v-model="form.resource">-->
<!--                  <el-radio label="Sponsor" />-->
<!--                  <el-radio label="Venue" />-->
<!--                </el-radio-group>-->
<!--              </el-form-item>-->
              <el-form-item label="活动内容描述">
                <el-input v-model="form.desc" type="textarea" />
              </el-form-item>
              <el-form-item>
                <el-button type="primary" @click="onSubmit">Create</el-button>
                <el-button>Cancel</el-button>
              </el-form-item>
            </el-tab-pane>

<!--            <el-tab-pane :label="`基本信息(${unrMessage.length})`" name="first">-->
<!--              <el-table :data="unrMessage" max-height="390px" :show-header="false" :row-style="{-->
<!--                height: '41.1px',-->
<!--              }">-->
<!--                <el-table-column label="内容" width="820" prop="content">-->
<!--                </el-table-column>-->
<!--                <el-table-column label="时间" width="200" prop="time">-->
<!--                </el-table-column>-->
<!--                <el-table-column label="操作" width="127">-->
<!--                  <template #default="scope">-->
<!--                    <el-button @click="read(scope.row)">标为已读</el-button>-->
<!--                  </template>-->
<!--                </el-table-column>-->
<!--              </el-table>-->
<!--              <el-button type="primary" class="confirm-btn" @click="readAll">全部标为已读</el-button>-->
<!--            </el-tab-pane>-->

            <!-- 已读消息 -->
            <el-tab-pane :label="`Step2:填写候选人信息`" name="second">
              <el-form :model="form" >
                <el-form-item label="候选人姓名">
                  <el-input v-model="form.name" />
                </el-form-item>
                <el-form-item label="手机号码">
                  <el-input v-model="form.telephone" />
                </el-form-item>
              </el-form>
              <el-form-item label="候选人描述">
                <el-input v-model="form.desc" type="textarea" />
              </el-form-item>
              <el-upload
                  class="avatar-uploader"
                  action="https://run.mocky.io/v3/9d059bf9-4660-45f2-925d-ce80ad6c4d15"
                  :show-file-list="false"
                  :on-success="handleAvatarSuccess"
                  :before-upload="beforeAvatarUpload"
              >
                <img v-if="imageUrl" :src="imageUrl" class="avatar" />
                <el-icon v-else class="avatar-uploader-icon"><Plus /></el-icon>
              </el-upload>
              <el-form-item>
                <el-button type="primary" @click="onSubmit">Create</el-button>
                <el-button>Cancel</el-button>
              </el-form-item>

<!--              <el-table :data="rMessage" max-height="390px" :show-header="false" :row-style="{-->
<!--                height: '41.1px',-->
<!--              }">-->
<!--                <el-table-column label="内容" width="820" prop="content">-->
<!--                </el-table-column>-->
<!--                <el-table-column label="时间" width="200" prop="time">-->
<!--                </el-table-column>-->
<!--                <el-table-column label="操作" width="127">-->
<!--                  <template #default="scope">-->
<!--                    <el-button @click="deleteMessage(scope.row)" type="danger">删除</el-button>-->
<!--                  </template>-->
<!--                </el-table-column>-->
<!--              </el-table>-->
<!--              <el-button type="danger" class="confirm-btn" @click="deleteAll">删除全部</el-button>-->
            </el-tab-pane>
            <!-- 回收站 -->
            <el-tab-pane :label="`活动预览`" name="third">
              <el-descriptions title="活动信息" :data="rec" max-height="490px" :show-header="false" :row-style="{
                height: '41.1px',
              }">
                <el-descriptions-item label="活动名称">1班优秀团员投票活动</el-descriptions-item>
                <el-descriptions-item label="活动区域">西安</el-descriptions-item>
                <el-descriptions-item label="活动时间">2023-5-30-07:30:00——2023-5-30-08:30:00</el-descriptions-item>

                <el-descriptions-item label="活动类型">
                  <el-tag size="small">特定场景</el-tag>
                </el-descriptions-item>
                <el-descriptions-item label="活动内容描述"
                >评选对象：全日制在校团员青年。
                  评选要求:1.积极参加团建创新活动;2.具有良好的群众基础;3.学习成绩良好以上。</el-descriptions-item
                >

                <el-descriptions-item label="候选人名称">张三、李四、小明、小美</el-descriptions-item>

                <el-descriptions-item label="候选人电话号码">13031 13032 13033 13034</el-descriptions-item>
                <el-descriptions-item label="候选人描述">张三:男，勤奋学习，名列前茅
                  李四:男，热爱运动，获省级奖励
                  小芳:女，多才多艺，有领导力
                  小美：女，发多篇论文，主持大创项目</el-descriptions-item>

              </el-descriptions>
              <el-row class="mb-4">
                <el-button type="success" text @click="dialogVisible = true">
                  Success
                </el-button>
                <el-dialog
                    v-model="dialogVisible"
                    title="提示"
                    width="30%"
                    :before-close="handleClose"
                >
                  <span>活动发布成功！</span>
                  <template #footer>
      <span class="dialog-footer">
        <el-button @click="dialogVisible = false">取消</el-button>
        <el-button type="primary" @click="dialogVisible = false">
          确认
        </el-button>
      </span>
                  </template>
                </el-dialog>
              </el-row>
              <el-table :data="rec" max-height="390px" :show-header="false" :row-style="{
                height: '41.1px',
              }">

<!--                <el-table-column label="内容" width="820" prop="content">-->
<!--                </el-table-column>-->
<!--                <el-table-column label="时间" width="200" prop="time">-->
<!--                </el-table-column>-->
<!--                <el-table-column label="操作" width="127">-->
<!--                  <template #default="scope">-->
<!--                    <el-button @click="recover(scope.row)">还原</el-button>-->
<!--                  </template>-->
<!--                </el-table-column>-->
              </el-table>
<!--              <el-button type="danger" class="confirm-btn" @click="clearRec">清空回收站</el-button>-->
            </el-tab-pane>
          </el-tabs>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script setup lang="ts">
import { ElMessageBox } from 'element-plus'

const dialogVisible = ref(false)

const handleClose = (done: () => void) => {
  ElMessageBox.confirm('您确定关闭此对话框吗?')
      .then(() => {
        done()
      })
      .catch(() => {
        // catch error
      })
}

import { ref, reactive, watch } from "vue";
import { getMessage, changeMsgStatus, delMsg, recoverMsg } from "../util/api";
import { Message } from "../model/home";
import { useMessageStore } from "../store/message";
import { confirm, message } from "../util/util"
const current = ref<string>("first");
import type { TabsPaneContext } from 'element-plus'
const activeName = ref('first')
import { ElMessage } from 'element-plus'
import { Plus } from '@element-plus/icons-vue'

import type { UploadProps } from 'element-plus'

const value1 = ref<[Date, Date]>([
  new Date(2000, 10, 10, 10, 10),
  new Date(2000, 10, 11, 10, 10),
])

const value2 = ref('')

const shortcuts = [
  {
    text: 'Last week',
    value: () => {
      const end = new Date()
      const start = new Date()
      start.setTime(start.getTime() - 3600 * 1000 * 24 * 7)
      return [start, end]
    },
  },
  {
    text: 'Last month',
    value: () => {
      const end = new Date()
      const start = new Date()
      start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)
      return [start, end]
    },
  },
  {
    text: 'Last 3 months',
    value: () => {
      const end = new Date()
      const start = new Date()
      start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)
      return [start, end]
    },
  },
]

const handleAvatarSuccess: UploadProps['onSuccess'] = (
    response,
    uploadFile
) => {
  imageUrl.value = URL.createObjectURL(uploadFile.raw!)
}

const beforeAvatarUpload: UploadProps['beforeUpload'] = (rawFile) => {
  if (rawFile.type !== 'image/jpeg') {
    ElMessage.error('Avatar picture must be JPG format!')
    return false
  } else if (rawFile.size / 1024 / 1024 > 2) {
    ElMessage.error('Avatar picture size can not exceed 2MB!')
    return false
  }
  return true
}

const imageUrl = ref('')

const handleClick = (tab: TabsPaneContext, event: Event) => {
  console.log(tab, event)
}
//已读消息
const rMessage = reactive<Message[]>([]);
//未读消息
const unrMessage = reactive<Message[]>([]);
//回收站
const rec = reactive<Message[]>([]);

const messages = useMessageStore();
//获取数据
const getData = () => {
  getMessage().then((response: any) => {
    const {
      data: {
        data: { read, unRead, recycle },
      },
    } = response;
    if (rMessage.length != 0) {
      rMessage.splice(0)
      unrMessage.splice(0);
      rec.splice(0)
    }
    (read as Message[]).forEach((e) => {
      rMessage.push(e);
    });
    (unRead as Message[]).forEach((e) => {
      unrMessage.push(e);
    });
    (recycle as Message[]).forEach((e) => {
      rec.push(e);
    });
  });
}
getData()
//标为已读
const read = (row: Message): void => {
  confirm("是否将消息标为已读", "设为已读", () => {
    changeMsgStatus(row.id).then((response: any) => {
      if (response) {
        const {
          data: { code, msg },
        } = response;

        if (code == "200") {
          getData();
          message("success", msg)
        } else {
          message("success", "修改失败")
        }
      }
    });
  })
};

//全部标为已读
const readAll = (): void => {
  confirm("是否将所有消息标为已读", "设为已读", () => {
    changeMsgStatus().then((response: any) => {
      if (response) {
        const {
          data: { code, msg },
        } = response;
        if (code == "200") {
          //刷新消息
          getData();
          message("success", msg)
        } else {
          message("success", "修改失败")
        }
      }
    });
  })
};

//删除
const deleteMessage = (row: Message): void => {
  confirm("删除消息", "是否要将这条消息删除", () => {
    delMsg(row.id).then((response: any) => {
      if (response) {
        const {
          data: { code, msg },
        } = response;

        if (code == "200") {
          getData();
          message("success", msg)
        } else {
          message("success", "网络错误")
        }
      }
    });
  })

};

const deleteAll = (): void => {
  confirm("删除全部消息", "是否要将所有消息删除", () => {
    delMsg().then((response: any) => {
      if (response) {
        const {
          data: { code, msg },
        } = response;

        if (code == "200") {
          getData();
          message("success", msg)
        } else {
          message("success", "网络错误")
        }
      }
    });
  })
};

//恢复
const recover = (row: Message): void => {
  confirm("是否要复原这条消息?", "复原消息", () => {
    recoverMsg(row.id).then((response: any) => {
      if (response) {
        const {
          data: { code, msg },
        } = response;

        if (code == "200") {
          getData();
          message("success", msg)
        } else {
          message("success", "网络错误")
        }
      }
    });
  })
};

//清空回收站
const clearRec = (): void => {
  confirm("是否要清空回收箱?", "清空回收箱", () => {
    recoverMsg().then((response: any) => {
      if (response) {
        const {
          data: { code, msg },
        } = response;

        if (code == "200") {
          getData();
          message("success", msg)
        } else {
          message("success", "网络错误")
        }
      }
    });
  })
};

watch(
  () => unrMessage.length,
  (newVal) => {
    messages.unReadNum = newVal;
  }
);

const form = reactive({
  telephone:'',
  name: '',
  region: '',
  date1: '',
  date2: '',
  delivery: false,
  type: [],
  resource: '',
  desc: '',
})
const onSubmit = () => {
  console.log('submit!')
}
</script>

<style scoped lang="less">
.dialog-footer button:first-child {
  margin-right: 10px;
}
.message-container {
  height: 85vh;
  padding: 10px;
  background-color: rgb(240, 240, 240);

  .el-card {
    padding: 30px 30px 0;

    .confirm-btn {
      margin: 30px 0 0 0;
    }
  }
}
demo-tabs > .el-tabs__content {
  padding: 32px;
  color: #6b778c;
  font-size: 32px;
  font-weight: 600;
}
</style>
<style scoped>
.avatar-uploader .avatar {
  width: 178px;
  height: 178px;
  display: block;
}
</style>

<style>
.avatar-uploader .el-upload {
  border: 1px dashed var(--el-border-color);
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;
  transition: var(--el-transition-duration-fast);
}

.avatar-uploader .el-upload:hover {
  border-color: var(--el-color-primary);
}

.el-icon.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  text-align: center;
}

.block {
  padding: 30px 0;
  text-align: center;
  border-right: solid 1px var(--el-border-color);
  flex: 1;
}
.block:last-child {
  border-right: none;
}
.block .demonstration {
  display: block;
  color: var(--el-text-color-secondary);
  font-size: 14px;
  margin-bottom: 20px;
}
</style>
