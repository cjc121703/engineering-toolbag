<template>
    <div>
        <v-stage :config="configKonva">
            <v-layer>
                <v-image :config="{
                        image: image,
                        width:imageWidth,
                        height:imageHeight
                    }"/>
                <v-line :config="configLine"></v-line>
                <v-rect :config="configPoint"></v-rect>
            </v-layer>
        </v-stage>
    </div>
</template>
<script>
export default {
    name: 'DrawLinesOnAPicture',
    props: [
        'imageSrc',
        'imageHeight',
        'imageWidth',
        'configPoint'
    ],
    data () {
        return{
            image: null,
            configKonva: null,
            configLine: {
                x: 0    ,
                y: 300,
                points: [0, 0, 300, 40, 25, 25],
                stroke: 'black'
            }
        }
    },
    created() {
        const image = new window.Image();
        image.src = this.imageSrc;
        this.configKonva = {
            width: this.imageHeight,
            height: this.imageWidth
        };
        image.onload = () => {
            // set image only when it is loaded
            this.image = image;
        };
    }
}
</script>

<style>

</style>
