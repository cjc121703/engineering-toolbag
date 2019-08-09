<template>
    <div>
        <v-stage ref="imgToDrawOn" :config="configKonva">
            <v-layer>
                <v-image 
                    @click="clickedTheImage"
                    :config="{
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
                <div
                    v-for="(curve, index) in curves"
                    :key="index"
                >
                    <quad-curve
                        :curve = curve
                    >
                        curve.startX
                    </quad-curve>
                </div>
                <div
                    v-for="(arc, index) in arcs"
                    :key="index"
                >
                    <v-arc
                        :config="arc"
                    >
                    </v-arc>
                </div>
            </v-layer>
        </v-stage>
    </div>
</template>
<script>
import QuadCurve from "@/components/QuadraticCurve";

export default {
    name: 'DrawLinesOnAPicture',
    props: [
        'imageSrc',
        'imageHeight',
        'imageWidth',
        'points',
        'lines',
        'curves',
        'arcs'
    ],
    components:{
        QuadCurve
    },
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
    },
    methods:{
        clickedTheImage(event) {
            const mousePos = this.$refs.imgToDrawOn.getStage().getPointerPosition();
            console.log('x:' +mousePos.x +' ,y:' + mousePos.y);
            this.$emit('clicked', mousePos);
        }
    }
}
</script>

<style>

</style>
