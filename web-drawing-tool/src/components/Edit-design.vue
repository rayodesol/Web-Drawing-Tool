<template>
    <v-container class="overflow-y-auto">
        <p><b>배경 서식</b></p>
        
        <v-row dense>
            <v-col cols="6">배경 색</v-col>
            <v-col cols="6">
                <v-color-picker
                    class = "background_color"
                    dot-size="10"
                    hide-canvas
                    hide-inputs
                    hide-mode-switch
                    swatches-max-height="100"
                ></v-color-picker>
            </v-col>
        </v-row>

        <v-row dense>
            <v-col cols="6">배경 무늬</v-col>
            <v-col cols="6" class = "a">
                <v-radio-group v-model="column" column>
                    <v-radio
                    label="무늬 없음"
                    value="radio-1"
                    ></v-radio>
                    <v-radio
                    label="격자 무늬"
                    value="radio-2"
                    ></v-radio>
                </v-radio-group>
            </v-col>
        </v-row>
        
        <p></p>
        <v-divider></v-divider>
        <p></p>
        
        <!--------------------------- 1 ---------------------------->
        <p><b>객체 서식</b></p>

        <v-sheet
            class="mx-auto"
            elevation="3"
            max-width="380"
        >
            <v-slide-group
                v-model="model"
                class="pa-4"
                active-class="success"
                show-arrows
                center-active
            >
                <v-slide-item
                    v-for="n in 10"
                    :key="n"
                    v-slot="{ active, toggle }"
                >
                    <v-card
                        :color="active ? undefined : 'grey lighten-1'"
                        class="ma-4"
                        height="50"
                        width="50"
                        @click="toggle"
                    >
                        <v-row
                            class="fill-height"
                            align="end"
                            justify="center"
                        >
                            <v-scale-transition>
                                <v-icon
                                    v-if="active"
                                    color="white"
                                    size="20"
                                    v-text="'mdi-check-circle-outline'"
                                ></v-icon>
                            </v-scale-transition>
                        </v-row>
                    </v-card>
                </v-slide-item>
            </v-slide-group>
        </v-sheet>
        <!------------------------- 1 ------------------------------>

        <p></p>
        <v-divider></v-divider>
        <p></p>

        <!------------------------- 2 ------------------------------>
        <p><b>선</b></p>

        <v-row dense>
            <v-col cols="6">
                <!--선 종류 selects-->
                <v-select class="line_type" :items="line_type" label="선 종류" outlined rounded>
                    <template v-slot:selection="{ item }">
                        <img :src="item.image" width="50">
                    </template>
                    <template v-slot:item="{ item }">
                        <img :src="item.image" width="50">
                    </template>
                </v-select>
                <!--선 종류 overflow buttons-->
                <!--------------------------------------------- 원래 코드
                <v-overflow-btn
                class = "line_type"
                :items="line_type"
                label="선 종류"
                rounded
                outlined
                ></v-overflow-btn>
                -->
            </v-col>

            <v-col cols="6">
                <!--선 두께 selects-->
                <v-select
                    class="line_thickness"
                    v-model="select" :items="line_weight" item-value="text"
                    label="선 굵기" outlined rounded>
                </v-select>
                <!--선 두께 overflow buttons-->
                <!--------------------------------------------- 원래 코드
                <v-overflow-btn
                class = "line_thickness"
                :items="line_weight"
                label="1pt"
                rounded
                outlined
                ></v-overflow-btn>
                -->
            </v-col>
        </v-row>

        <v-row dense>
            <v-col cols="6">
                선 색상
                <v-color-picker
                    class = "line_color" 
                    dot-size="10"
                    hide-canvas
                    hide-inputs
                    hide-mode-switch
                    swatches-max-height="100"
                ></v-color-picker>
            </v-col>
        </v-row>
        <!------------------------ 2 ------------------------------->

        <p></p>
        <v-divider></v-divider>
        <p></p>

        <!------------------------- 3 ------------------------------>
        <p><b>채우기</b></p>
        
        <v-row>
            <v-col cols="6">
                <!--무늬 종류 selects-->
                <v-select class="paint_type" :items="pattern_type" label="무늬 종류" outlined rounded>
                </v-select>
                <!--무늬 종류 overflow buttons-->
                <!--------------------------------------------- 원래 코드
                <v-overflow-btn
                class = "paint_type"
                :items="pattern_type"
                label="무늬 종류"
                rounded
                outlined
                ></v-overflow-btn>
                -->
            </v-col>

            <v-col cols="6">
                <v-color-picker 
                    class = "paint_color"
                    dot-size="10"
                    hide-canvas
                    hide-inputs
                    hide-mode-switch
                    swatches-max-height="100"
                ></v-color-picker>
            </v-col>
        </v-row>
        <!-------------------------- 3 ----------------------------->
        <!------------------------------test------------------------------------>
        <v-row>
        <v-col cols="6">
            <!--무늬 종류 selects-->
            <v-select class="paint_type" :items="pattern_types" label="무늬 종류" outlined rounded>
                <template v-slot:selection="{ item }">
                    <img :src="item.image" width="50">
                </template>
                <template v-slot:item="{ item }">
                    <img :src="item.image" width="50">
                </template>
            </v-select>
        </v-col>
        </v-row>
        <!------------------------------test------------------------------------>
    </v-container>
</template>

<script>
export default {
    name: 'Edit-design',

    data: () => ({
        column: null,

        line_type: [
            { image: require("@/assets/Edit icons/line_horizontal_regular_icon_203504.svg") },
            { image: require("@/assets/Edit icons/line_dashed_icon_125233.svg") },
            //{ image: require("@/assets/dotted_icon.svg") },
            { image: require("@/assets/Edit icons/line_double_icon_125231.svg") },

            //{ image: require("@/assets/solid_style_border_icon_214487.svg") },
            //{ image: require("@/assets/line_icon_126358.svg") },
            //{ image: require("@/assets/line_dotted_icon.svg") },
            //{ image: require("@/assets/dashed_icon_212310.svg") },
            
        ],

        line_weight: [
            '1pt', '2pt', '3pt', '4pt', '5pt', '6pt', '7pt', '8pt', '9pt', '10pt',
        ],
        select: { text: '1pt' },

        pattern_type: [
            { text: '무늬 없음' },
            { text: '수평선' },
            { text: '수직선' },
            { text: '눈금무늬' },
        ],
        
        pattern_types: [
            //{ image: require("@/assets/Edit icons/.svg") },
            //{ image: require("@/assets/Edit icons/.svg") },
            //{ image: require("@/assets/Edit icons/.svg") },
            { text: "무늬 없음" },
            { image: require("@/assets/reorder_117573.svg") },
            { image: require("@/assets/reorder_vertical_icon_137250.svg") },
            { image: require("@/assets/grid_view_icon_212682.svg") },
        ],
    }),
}
</script>

<style scoped>
div {
    max-width: 400px;
    max-height: 600px;
}
.background_color{
    background-color: #EEEEEE;
    /*width: 150px;*/
    height: 100px;
}
.line_color{
    background-color: #EEEEEE;
    height: 100px;
}
.paint_color{
    background-color: #EEEEEE;
    height: 100px;
}
/*
.line_type{
    width: 160px;
}
.line_thickness{
    width: 130px;
}
.paint_type{
    width: 200px;
}
*/
</style>