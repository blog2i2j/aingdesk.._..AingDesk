<template>
    <n-modal :show="createAgentShow" preset="card" :title="$t('创建智能体')" style="width: 540px;" :show-icon="false" :closable="false">
        <n-form :model="createAgentFormData" :rules="rules" ref="createAgentModelRef">
            <n-form-item :label="$t('名称')" path="agent_title">
                <n-input :placeholder="$t('请输入智能体名称')" v-model:value="createAgentFormData.agent_title" />
            </n-form-item>
            <n-form-item :label="$t('人物设定')" path="prompt">
                <n-input :placeholder="$t('你是经过中国法律数据库训练的专业法律AI，熟悉民法典,刑法,商法等主要法律体系，支持合同审查,法律条文解读,诉讼策略建议，严格区分法律咨询与律师服务边界')" type="textarea" v-model:value="createAgentFormData.prompt" />
            </n-form-item>
            <n-form-item :label="$t('头像')" path="icon">
                <n-popover trigger="click" v-model:show="choosePicVisible">
                    <template #trigger>
                        <n-button @click="choosePicVisible = true">{{
                            createAgentFormData.icon ? createAgentFormData.icon : $t("请选择") }}</n-button>
                    </template>
                    <EmojiPicker @select="choosePic" :native="true"/>
                </n-popover>
            </n-form-item>
        </n-form>

        <template #action>
            <div class="flex justify-end gap-5">
                <n-button @click="cancelCreateAgent">{{ $t("取消") }}</n-button>
                <n-button type="primary" @click="createAgent" v-if="!isEditAgent">{{ $t("确认") }}</n-button>
                <n-button type="primary" @click="modifyAgent" v-else>{{ $t("保存") }}</n-button>
            </div>
        </template>
    </n-modal>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import { getAgentStoreData } from '../store';
import { useI18n } from 'vue-i18n';
import EmojiPicker from 'vue3-emoji-picker'
import 'vue3-emoji-picker/css'
import { createAgent,modifyAgent } from '@/views/Agent/controller';
const { t: $t } = useI18n()
const { createAgentShow, createAgentFormData, isEditAgent } = getAgentStoreData()
const choosePicVisible = ref(false) // 选择头像
const rules = ref({
    ragName: [{ required: true, message: $t('请输入智能体名称'), trigger: 'blur' }],
    ragDesc: [{ required: true, message: $t('请为您的智能体设定提示词'), trigger: 'blur' }],
})
const createAgentModelRef = ref()

/**
 * 
 * @description 选择头像头的回调
 */
function choosePic(emojiRes: any) {
    createAgentFormData.value.icon = emojiRes.i as string;
}

/**
 * @description 取消创建智能体
 */
function cancelCreateAgent() {
    createAgentShow.value = false
    createAgentFormData.value = {
        agent_type: "",
        agent_name: "",
        agent_title: "",
        prompt: "",
        icon: ""
    }
    isEditAgent.value = false
}


</script>

<style scoped></style>