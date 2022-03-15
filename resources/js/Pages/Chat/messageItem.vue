<template>
    <div>
        <span>{{ message.user.name }}: {{ message.message }}</span>
    </div>
</template>

<script>

export default {
    props: ['message']
}
</script>