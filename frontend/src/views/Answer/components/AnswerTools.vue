<template>
    <div class="tools">
        <n-tooltip>
            <template #trigger>
                <span class="tool-item" @click="copyContent(answerContent.content as string)"><i
                        class="i-common:copy w-20 h-20"></i></span>
            </template>
            {{ $t("复制") }}
        </n-tooltip>
        <n-tooltip>
            <template #trigger>
                <span class="tool-item"><i class="i-common:attention w-20 h-20"></i></span>
            </template>
            <div class="flex justify-center items-start flex-col info-pop" v-if="(answerContent.stat as Stat)!.eval_count">
                <div>
                    <span>eval count: </span>{{ (answerContent.stat as Stat)!.eval_count }}
                </div>
                <div>
                    <span>model: </span>{{ (answerContent.stat as Stat)!.model }}
                </div>
                <div>
                    <span>created at: </span>
                    {{ isoToLocalDateTime((answerContent.stat as Stat)!.created_at as string) }}
                </div>
                <div>
                    <span>total duration: </span>
                    {{ fixedStrNum((answerContent.stat as Stat)!.total_duration as string) }}s
                </div>
                <div>
                    <span>load duration: </span>
                    {{ fixedStrNum((answerContent.stat as Stat)!.load_duration as string) }}ms
                </div>
                <div>
                    <span>prompt eval count: </span>
                    {{ (answerContent.stat as Stat)!.prompt_eval_count }}
                </div>
                <div>
                    <span>prompt eval duration: </span>
                    {{ fixedStrNum((answerContent.stat as Stat)!.prompt_eval_duration as string) }}ms
                </div>
                <div>
                    <span>eval duration: </span>
                    {{ fixedStrNum((answerContent.stat as Stat)!.eval_duration as string) }}s
                </div>
            </div>
            <div v-else>{{ $t("暂无信息") }}</div>
        </n-tooltip>
        <n-tooltip>
            <template #trigger>
                <span class="tool-item" @click="answerAgain(questionContent, answerContent.id as string)"><i
                        class="i-common:refresh w-20 h-20"></i></span>
            </template>
            {{ $t("重新生成") }}
        </n-tooltip>
    </div>
</template>

<script setup lang="ts">
import { isoToLocalDateTime, fixedStrNum } from "@/utils/tools"
import { answerAgain, copyContent } from "@/views/Answer/controller"
import type { AnswerInfo, MultipeQuestionDto, Stat } from '@/views/Home/dto';

defineProps<{ answerContent: AnswerInfo, questionContent: MultipeQuestionDto }>()
</script>

<style scoped></style>