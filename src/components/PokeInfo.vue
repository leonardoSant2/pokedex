<template>
    <div>
        <h1>{{num}} {{ upper }}</h1>
    <small>{{ url }}</small>
    </div>
</template>

<script>
export default {
    props: {
        num: Number,
        name: String,
        url: String
    },
    methods: {
    capitalized(name) {
      const capitalizedFirst = name[0].toUpperCase();
      const rest = name.slice(1);
      return capitalizedFirst + rest;
    }
    },
    computed: {
        upper() {
      return this.capitalized(this.name);
    }
}
}
</script>

<style>

</style>