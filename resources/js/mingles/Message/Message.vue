<script setup>
import {useToast} from '@/components/ui/toast/use-toast'
import {useMouse} from '@/composables/useMouse'
import useMessage from '@/composables/useMessage'
import {Input} from '@/components/ui/input'
import {Button} from '@/components/ui/button'

const {toast} = useToast()

const props = defineProps({
    wire: {},
    wireId: {},
    mingleData: {},
})

const {message} = useMessage()

message.value = props.mingleData.message

const {x, y} = useMouse()

const save = () => {
    props.wire.save(message.value)
        .then(() => {
            toast({
                title: 'Success!',
                description: 'Succesfully saved message',
            })
        })
        .catch(() => {
            toast({
                title: 'Error!',
                description: 'Failed to save message',
            })
        })
}

</script>

<template>
    <div class="my-10 bg-cyan-300 rounded-xl p-4">
        <div>
            Message
        </div>
        <div class="flex gap-4 my-4">
            <Input v-model="message"/>
            <Button @click="save" class="min-w-24"> Save</Button>
        </div>
        <p v-text="message"/>
        <div>
            <p>Mouse position is at: {{ x }}, {{ y }}</p>
        </div>

    </div>
</template>
