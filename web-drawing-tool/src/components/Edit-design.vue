<template>
    <v-container>
        <p>배경 서식</p>
        <v-row dense>
            <v-col cols="6">배경 색</v-col>
            <v-col cols="6">색상 선택 바???</v-col>
        </v-row>

        <v-row dense>
            <v-col cols="6">배경 무늬</v-col>
            <v-col cols="6">
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
        
        <p>객체 서식</p>

        <p></p>
        <v-divider></v-divider>
        <p></p>

        <p>선</p>
        <!------------------------------------------------------->
        <v-row>
            <v-col cols="6" md="4">선 종류</v-col>
            <v-col cols="6" md="4">두께</v-col>
            <v-col cols="6" md="4">색상 선택 바???</v-col>
        </v-row>
        <!------------------------------------------------------->

        <p></p>
        <v-divider></v-divider>
        <p></p>

        채우기
    </v-container>
</template>

<script>
export default {
    name: 'Edit-design',

    data () {
        return {
            column: null,
        }
    },
}
</script>