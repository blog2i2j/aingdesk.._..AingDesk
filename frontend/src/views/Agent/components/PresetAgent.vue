<template>
    <div class="flex flex-wrap gap-5 justify-start items-center">
        <n-card hoverable class="w-200 cursor-pointer" v-for="item in systemAgentList" :key="item.create_time"
            @click="chooseAgentForChat(item)">
            <div class="flex justify-between items-center">
                <div class="agent-card">
                    <span class="emoji-span mr-10">{{ item.icon ? item.icon : "😀" }}</span>
                    <span class="text">{{
                        item.agent_title
                    }}</span>
                </div>
            </div>
        </n-card>
    </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';
import { getAgentStoreData } from '@/views/Agent/store';
import {
    chooseAgentForChat
} from "@/views/Agent/controller"
const {
    agentList,
} = getAgentStoreData()
// 系统预设智能体列表
const systemAgentList = computed(() => agentList.value.filter(item => item.is_system))
</script>

<style scoped></style>