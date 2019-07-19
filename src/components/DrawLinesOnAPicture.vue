<template>
    <div>
        <v-stage :config="configKonva">
            <v-layer>
                <v-image :config="{
                        image: image,
                        width:imageWidth,
                        height:imageHeight
                    }"/>
                <div
                    v-for="(point, index) in points"
                    :key="index"
                >
                    <v-rect :config="point"></v-rect>
                </div>
                <div
                    v-for="(line, index) in lines"
                    :key="index"
                >
                    <v-line :config="line"></v-line>
                </div>
                

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
        'points',
        'lines'
    ],
    data () {
        return{
            image: null,
            configKonva: null
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
