<template>
    <div class="out" scrolling="no">
        <div style="height: 200px ">
            <el-row :gutter="20"  class="el-row" type="flex">
                <el-col :span="8" >
                    <el-card :body-style="{ padding: '0px' }" style="width: 300px;">
                        <img src='../../assets/image/icon/old.jpg' class="image" >
                        <div style="padding-top:50px;float: left;width: 40%">
                            <span style="font-weight:bold">老人姓名:</span>
                            <p >陈瑞婷</p>
                        </div>
                    </el-card>
                </el-col>
                <el-col :span="8" >
                    <el-card :body-style="{ padding: '0px' }" style="width: 300px;">
                        <img src='../../assets/image/icon/smile.jpg' class="image" >
                        <div style="padding-top:50px;float: left;width: 40%">
                            <span style="font-weight:bold">情感检测</span>
                            <p >微笑：0次</p>
                            <p >哭泣：0次</p>
                        </div>
                    </el-card>
                </el-col>

                <el-col :span="8" >
                    <el-card :body-style="{ padding: '0px' }" style="width: 300px;">
                        <img src='../../assets/image/icon/fall.jpg' class="image" >
                        <div style="padding-top:50px;float: left;width: 40%">
                            <span style="font-weight:bold">摔倒检测</span>
                            <p >摔倒：0次</p>
                        </div>
                    </el-card>
                </el-col>
                <el-col :span="8" >
                    <el-card :body-style="{ padding: '0px' }" style="width: 300px;">
                        <img src='../../assets/image/icon/exit.jpg' class="image" >
                        <div style="padding-top:50px;float: left;width: 40%">
                            <span style="font-weight:bold">禁止区入侵</span>
                            <p >出现：0次</p>
                        </div>
                    </el-card>
                </el-col>
                <el-col :span="8" >
                    <el-card :body-style="{ padding: '0px' }" style="width: 300px;">
                        <img src='../../assets/image/icon/vol.jpg' class="image" >
                        <div style="padding-top:50px;float: left;width: 40%">
                            <span style="font-weight:bold">义工交互</span>
                            <p >出现：0次</p>
                        </div>
                    </el-card>
                </el-col>
            </el-row>

        </div>
        <div style="margin-top: 20px;margin-bottom: 50px" >
            <iframe class="camera" src="http://127.0.0.1:5001" scrolling="no" ></iframe>
            <el-row :gutter="20"  class="el-row" type="flex">
                <el-col :span="8" >
                    <div id="chartPie"  style="width: 600px;height: 500px;margin-left: 150px"></div>
                </el-col>

                <el-col :span="8" >
                    <div id="myChart" style="width: 600px;height: 500px;margin-left: 270px"></div>
                </el-col>
            </el-row>


        </div>


    </div>
</template>

<script>
    import * as echarts from 'echarts';


    export default {
        name: "InfoDetial",
        components: {


        },
        data() {
            return {

                chartPie: null,
                chartBar:null,
            };
        },
        mounted(){
            this.$nextTick(() => {
                this.drawPieChart();
            })

            this.drawBarChart();

        },
        methods:{
            drawPieChart() {
                let mytextStyle = {
                    color: "#333",
                    fontSize: 18,
                };
                let mylabel = {
                    show: true,
                    position: "right",
                    offset: [30, 40],
                    formatter: '{b} : {c} ({d}%)',
                    textStyle: mytextStyle
                };
                this.chartPie = echarts.init(document.getElementById('chartPie'),'walden');
                this.chartPie.setOption({
                    title: {
                        text: '数据分析',
                        subtext: '老人情感',
                        x: 'center'
                    },
                    tooltip: {
                        trigger: 'item',
                        formatter: "{a} <br/>{b} : {c} ({d}%)",
                    },
                    legend: {
                        data: ['微笑', '哭泣', '无表情'],
                        left:"center",
                        top:"bottom",
                        orient:"horizontal",
                    },
                    series: [
                        {
                            name: '访问来源',
                            type: 'pie',
                            radius: ['50%', '70%'],
                            center: ['50%', '50%'],
                            data: [
                                {value: 335, name: '微笑'},
                                {value: 310, name: '哭泣'},
                                {value: 234, name: '无表情'},
                            ],
                            animationEasing: 'cubicInOut',
                            animationDuration: 2600,
                            label: {
                                emphasis: mylabel
                            },


                        }
                    ]
                });
            },
            drawBarChart(){
                var myChart = this.$echarts.init(document.getElementById('myChart'));//获取容器元素
                var option = {
                    legend: {//图例
                        data: ['次数'],//与series的name对应
                        left: '75%',//图例的位置，可以用像素，可以用百分比，也可以用center，right等
                        top: 12.5,//图例的位置
                        itemWidth: 10,//图例图标的宽
                        itemHeight: 10,//图例图标的高
                        textStyle: {
                            color: '#878787',//值的具体的颜色
                        }
                    },
                    xAxis: {//x轴
                        type: 'category',
                        data: ['微笑', '摔倒', '陌生人', '义工'],//x轴的数据

                        // splitArea: {show: true},//保留网格区域
                        axisLine: {//坐标线
                            lineStyle: {
                                type: 'solid',
                                color: '#000000',//轴线的颜色
                                width:'1'//坐标线的宽度
                            }
                        },
                        axisTick: {//刻度
                            show: false//不显示刻度线
                        },
                        axisLabel: {
                            textStyle: {
                                color: '#878787',//坐标值的具体的颜色
                            }
                        },
                        splitLine: {
                            show: false//去掉分割线
                        },
                    },
                    backgroundColor: '#fff',//图得背景色
                    yAxis: {
                        name: '单位：次',//轴的名字，默认位置在y轴上方显示
                        max: 30,//最大刻度
                        type: 'value',
                        // axisLine: {//线
                        //     show: false
                        // },
                        axisTick: {//刻度
                            show: false
                        },
                        axisLabel: {
                            textStyle: {
                                color: '#878787',//坐标值得具体的颜色
                            }
                        },
                        minInterval: 5,//标值的最小间隔
                        splitLine: {
                            lineStyle: {
                                color: ['#f6f6f6'],//分割线的颜色
                            }
                        }
                    },
                    series: [{
                        name: '次数',//每组数据的名字，与图例对应
                        data: [20, 20, 22, 18],//数据
                        type: 'bar',//柱状图
                        itemStyle: {
                            normal: {
                                color: '#FD6B71',//设置柱子颜色
                                label: {
                                    show: true,//柱子上显示值
                                    position: 'top',//值在柱子上方显示
                                    textStyle: {
                                        color: '#FD6B71'//值得颜色
                                    }
                                }
                            }
                        },
                        barWidth: 30//设置柱子宽度，单位为px
                    }],
                };
                myChart.setOption(option);//设置option



            }
        }
    }
</script>

<style scoped>


    .image {

        float: left; width: 60%;
        height: 180px;
    }


    .out{
        padding-top: 50px;
        padding-left: 60px;


    }

    .camera{
        top:80px;
        margin-left: 450px;
        margin-bottom: 30px;
        width: 800px;
        height: 600px;
    }
</style>
