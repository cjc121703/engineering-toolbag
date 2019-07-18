<template>
    <div>
        <v-stage :config="configKonva">
            <v-layer>
                <v-image :config="{
                        image: image,
                        width:imageWidth,
                        height:imageHeight
                    }"/>
                <v-rect :config="configPoint"></v-rect>
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
        'configPoint',
        'lines'
    ],
    data () {
        return{
            image: null,
            configKonva: null,
            configLine: {
                x: 0,
                y: 0,
                points: [0,0,500,500],
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
