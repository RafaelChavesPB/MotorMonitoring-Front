<template>
    <div>
        <div>
            {{fakedata}}
        </div>
        <v-btn @click="update"> Append data </v-btn>
    </div>
</template>

<script>
export default {
    name: 'DataChart',
    data(){
        return {
            fakedata: [],
        }
    },
    methods:{
        update(){
            this.fakedata.push(this.getRandomNumber())
            if(this.fakedata.length > 40)
                this.fakedata.splice(0, 1)
        },
        getRandomNumber(){
            const max = 440;
            return Math.floor(Math.random()*(max))
        }
    }
}
</script>