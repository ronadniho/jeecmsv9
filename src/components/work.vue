<template>
  <div style="background:#ecf0f5">
      <el-row :gutter="24">
        <el-col :xs="24" :sm="12" :md="12" :lg="6" class="span24 index-flex">
          <div class="bg-box">
              <div class="bg-green bg-icon">
                    <span class="iconfont icon-neirong"></span>
                    <p class="icon-title">内容发布数</p>
              </div>
                <div class="bg-info">
                    <p class="today-count">今日&nbsp;&nbsp;<span class="count-num">{{page.pageNum.contentDayTotalCount}}&nbsp;</span>
                      <span class="up-num">({{page.pageNum.contentDayUncheckCount}})</span>
                    </p>
                  <p class="all-count">累计:&nbsp;&nbsp;{{page.pageNum.contentTotal}}</p>
                </div>
              </div>
          </el-col>
           <el-col :xs="24" :sm="12" :md="12" :lg="6" class="span24 index-flex">
              <div class="bg-box">
                <div class="bg-yellow bg-icon">
                    <span class="iconfont icon-pinglun-copy"></span>
                      <p class="icon-title">评论数</p>
                </div>
                  <div class="bg-info">
                    <p class="today-count">今日&nbsp;&nbsp;<span class="count-num">{{page.pageNum.commentDayTotalCount}}&nbsp;</span>
                      <span class="up-num">({{page.pageNum.commentDayUncheckCount}})</span>
                    </p>
                  <p class="all-count">累计:&nbsp;&nbsp;{{page.pageNum.commentTotal}}</p>
                </div>
              </div>
          </el-col>
           <el-col :xs="24" :sm="12" :md="12" :lg="6" class="span24 index-flex">
               <div class="bg-box ">
             <div class="bg-blue bg-icon">
                <span class="iconfont icon-liuyan"></span>
                  <p class="icon-title">留言数</p>
             </div>
                 <div class="bg-info">
                    <p class="today-count">今日&nbsp;&nbsp;<span class="count-num">{{page.pageNum.guestbookDayTotalCount}}</span>
                      <span class="up-num">({{page.pageNum.guestbookDayUncheckTotalCount}})</span>
                    </p>
                  <p class="all-count">累计:&nbsp;&nbsp;{{page.pageNum.guestbookTotal}}</p>
                </div>
                </div>
          </el-col>

           <el-col :xs="24" :sm="12" :md="12" :lg="6" class="span24 index-flex"> 
               <div class="bg-box">
                  <div class="bg-purple bg-icon">
                      <span class="iconfont icon-zhuce"></span>
                        <p class="icon-title">会员注册数</p>
                  </div>
                  <div class="bg-info">
                    <p class="today-count">今日&nbsp;&nbsp;<span class="count-num">{{page.pageNum.memberToday}}</span>
                      <span class="up-num"></span>
                    </p>
                  <p class="all-count">累计:&nbsp;&nbsp;{{page.pageNum.memberTotal}}</p>
                </div>
              </div>
          </el-col>
     </el-row>
        <el-row :gutter="24">
            <!--趋势分析-->
           <el-col :xs="24" :sm="24" :md="12" :lg="12" class="span24">
             <div class="h358">
               <div class="work-header">
                   <span>趋势分析</span>
                   <a href="javascript:void(0)" @click="routerLink('/traffic/trend','')" class="iconfont icon-gengduo"></a>
                </div>
                 <div class="work-body">
                    <div id="chartLine" style="height:308px"></div>
                </div>
             </div>
           </el-col>
             <!--来源分析-->
               <el-col :xs="24" :sm="24" :md="12" :lg="12" class="span24 ">
                  <div class="h358">
                    <div class="work-header">
                            <span>来源分析</span>
                            <a href="javascript:void(0)" @click="routerLink('/sourceanalysis/class','')" class="iconfont icon-gengduo"></a>
                      </div>
                        <div class="work-body">
                    <div id="chartPie" style="height:308px"></div>
                </div>
             </div>
           </el-col>
        </el-row>
        <!-- 搜索词 -->
         <el-row :gutter="24">
              <el-col :xs="24" :sm="24" :md="12" :lg="12" class="span24 ">
                  <div class="h440">
                      <div class="work-header">
                          <span>搜索词 Top 10</span>
                          <a href="javascript:void(0)"  @click="routerLink('/sourceanalysis/keywords','')" class="iconfont icon-gengduo"></a>
                        </div>
                        <div class="work-body">
                       <table class="index-table">
                         <tr>
                          <th class="text-left">搜索词</th>
                          <th class="text-right">浏览量(PV)</th>
                          <th class="text-right">占比</th>
                         </tr>
                          <tr v-for="(item,index) in page.keyword" :key="index">
                          <td class="text-left">{{index}}</td>
                          <td class="text-right">{{item}}</td>
                          <td class="text-right">{{((item/page.sumkey)*100).toFixed(1)}}%</td>
                         </tr>
                         
                       </table>
                </div>
                    </div>
               </el-col>
       
          <!-- 来访域名 -->

              <el-col :xs="24" :sm="24" :md="12" :lg="12" class="span24 ">
                  <div class="h440">
                      <div class="work-header">
                          <span>来访域名 Top 10</span>
                          <a href="javascript:void(0)" @click="routerLink('/sourceanalysis/domain','')" class="iconfont icon-gengduo"></a>
                        </div>
                         <div class="work-body">
                            <table class="index-table">
                              <tr>
                                <th class="text-left">来访域名</th>
                                <th class="text-right">浏览量(PV)</th>
                                <th class="text-right">占比</th>
                              </tr>
                              <tr v-for="(item,index) in page.source" :key="index">
                                <td class="text-left">{{index}}</td>
                                <td class="text-right">{{item}}</td>
                                <td class="text-right">{{((item/page.sum)*100).toFixed(1)}}%</td>
                              </tr>
                            </table>
                </div>
                    </div>
               </el-col>
         </el-row>
         <!-- 系统信息 -->
         <div class="systemInfo">
           <span>
              当前系统版本:&nbsp;&nbsp;jeecms v9   
           </span>
          <span>
              上次登录时间: &nbsp;&nbsp;{{page.pageNum.lastLoginTime}}
           </span>
           <span>
            已用内存: &nbsp;&nbsp;{{page.pageNum.usedMemory}}MB  
           </span>
           <span>
           剩余内存:&nbsp;&nbsp;{{page.pageNum.useableMemory}}MB   
           </span>
           <span>
             最大内存:&nbsp;&nbsp; {{page.pageNum.maxMemory}}MB
           </span>
         </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      chartLine: null,
      chartPie: null,
      params:{
        type:'source',  //查询分类
        flag:'1',  //查询范围
        target:'',  //查询指标
        year:'',  //年度
        begin:'',  //开始日期
        end:'',  //结束日期
        orderBy:'',  //排序
        count:'10',
      },
      page:{
          //页面数据
          source:[],  //来访域名  type:array
          keyword:[],  //搜索词   type:array
          pageNum:'',
          adminNum:'',//会员数
          pv:[],//获取pv、
          ip:[],//ip、
          fk:[], //访客数信息
          avg:[],//平均访问时长  
          wd:[],//时间维度
          ss:[],//来源分析
          ssKey:[],//来源键
          sum:'',
          sumkey:'',

      },
      chartLineOptions: {
        //折线图配置
        tooltip: {
          trigger: "axis"
        },
        legend: {
          data: ["pv统计", "ip统计", "独立访客统计"]
        },
        grid: {
          left: "5%",
          right: "2%",
          bottom: "14%"
        },
        xAxis: {
          type: "category",
          splitLine: { show: false },
          boundaryGap: false,
          data: ["周一", "周二", "周三", "周四", "周五", "周六", "周日"]
        },
        yAxis: {
          splitLine: { show: false },
          type: "value"
        },
        series: [
          {
            name: "pv统计",
            type: "line",
            showSymbol: false,
            smooth: true, //这句就是让曲线变平滑的

            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: "ip统计",
            type: "line",
            showSymbol: false,
            smooth: true, //这句就是让曲线变平滑的

            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: "独立访客统计",
            type: "line",
            showSymbol: false,
            smooth: true, //这句就是让曲线变平滑的
            data: [150, 232, 201, 154, 190, 330, 410]
          }
        ]
      },
      chartPieOptions: {
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)"
        },
        legend: {
          orient: "vertical",
          left: "right",
          data: ["直接访问", "邮件营销", "联盟广告", "视频广告", "搜索引擎"]
        },
        series: [
          {
            name: "来源分析",
            type: "pie",
            radius: "55%",
            radius: ["50%", "70%"],
            data: [
              { value: 335, name: "直接访问" },
              { value: 310, name: "邮件营销" },
              { value: 234, name: "联盟广告" },
              { value: 135, name: "视频广告" },
              { value: 1548, name: "搜索引擎" }
            ]
          }
        ],
        color: ["#56dea0", "#ffbe60", "#fa99cb", "#46d7e8", "#86c0e9"]
      }
    };
  },
  methods: {
    createChart(){//构造图表
   
        this.chartLine.resize();
         this.chartPie.resize();
    },
    create(type){
      //获取欢迎页面需要的数据 
          if(type==='link'){
              this.params.type=type;
              axios.post(this.$api.flowSourceList, this.params).then(res => {
                    this.page.source=res.body.totalMap; 
                    let sum=0;
                    for(let x in res.body.totalMap){
                          sum+=res.body.totalMap[x];                    
                    }  
                    if(sum===0){
                      sum=1;
                    }
                    this.page.sum=sum; 
                     this.create('keyword');            
                   
              })
              .catch(err => {
                this.loading = false;
              }); 
          }
          if(type==='keyword'){
               this.params.type=type;
                axios.post(this.$api.flowSourceList, this.params).then(res => {
                      this.page.keyword=res.body.totalMap;  
                       let sumkey=0;
                      for(let i in res.body.totalMap){
                          sumkey+=res.body.totalMap[i];                    
                      }  
                      if(sumkey===0){
                        sumkey=1;
                      }
                      this.page.sumkey=sumkey;        
                })
                .catch(err => {
                  this.loading = false;
                }); 
          }
          
    },
    globalCount(){
      //获取内容总数
        axios.post(this.$api.globalStatistic).then(res => {
              this.page.pageNum=res.body
        })
        .catch(err => {
          this.loading = false;
        });      
    },
    globalAdmin(){
      //获取会员注册数
        axios.post(this.$api.statisticMemberList,{queryModel:'month',begin:'',end:''}).then(res => {
              this.page.adminNum=res.body
        })
        .catch(err => {
          this.loading = false;
        });      
    },
     getsource(){
      //获取来源 
          let pam={
              type:'source',  //查询分类
              flag:'1',  //查询范围
              target:'0',  //查询指标
              year:'',  //年度
              begin:'',  //开始日期
              end:'',  //结束日期
              orderBy:'',  //排序
              count:'10',
          };
          axios.post(this.$api.flowSourceList, this.pam).then(res => {
               this.page.ss=res.body.totalMap;                         
                let ss=[];
                let a=0;
                for(let i in res.body.totalMap){   
                      let obj={
                          value:'',
                          name:'',
                      };                 
                      obj.name=res.body.keys[a];
                      obj.value=res.body.totalMap[i];
                    
                      ss.push(obj);
                      a++;                    
                }
            let sour = {
                  legend: {
                    orient: "vertical",
                    left: "right",
                    data: res.body.keys
                  },
                   series: [
                    {
                      name: "来源分析",
                      type: "pie",
                      radius: "55%",
                      radius: ["50%", "70%"],
                      data: ss
                    }
                  ],
                   color: ["#56dea0", "#ffbe60"]
            }
                this.chartPie.setOption(sour);

          })
          .catch(err => {
            this.loading = false;
          });         
    },
    getPv(){
      //获取pv、ip、访客数信息
        axios.post(this.$api.flowPvList,{flag:'4',begin:'',end:'',statisDay:'',year:''}).then(res => {
              this.page.pv=res.body;
              let list =res.body.list;
              let pv=[];
              let ip=[];
              let fk=[];
              let avg=[];
              let wd=[];
              let xData=[];
             
              for(let i in list){            
                  pv.push(list[i][0]);
                  ip.push(list[i][1]);
                  fk.push(list[i][2]);
                  avg.push(list[i][3]);
                  xData.push(this.timeFormat('day',list[i][4]));
              }
             
              let obj= {
                xAxis: {
                    data: xData
                },
                series:[ {
                    name: "pv统计",
                    type: "line",
                    showSymbol: false,
                    smooth: true, //这句就是让曲线变平滑的

                    data: pv
                  },
                  {
                    name: "ip统计",
                    type: "line",
                    showSymbol: false,
                    smooth: true, //这句就是让曲线变平滑的

                    data: ip
                  },
                  {
                    name: "独立访客统计",
                    type: "line",
                    showSymbol: false,
                    smooth: true, //这句就是让曲线变平滑的
                    data: fk
                  }
                ]
              }
              
              this.chartLine.setOption(obj);
     
        })
        .catch(err => {
          this.loading = false;
        });      
    },
    timeFormat(flag,timeName){//格式化时间显示
        let formatTime='0';
        if(flag=='day'||flag=='yesterday'){//小时转换
            switch (timeName) {
                case 0:
                formatTime="00:00-00:59" 
                    break;
                case 1:
                formatTime="01:00-01:59" 
                    break;
                    case 2:
                formatTime="02:00-02:59" 
                    break;
                    case 3:
                formatTime="03:00-03:59" 
                    break;
                    case 4:
                formatTime="04:00-04:59" 
                    break;
                    case 5:
                formatTime="05:00-05:59" 
                    break;
                    case 6:
                formatTime="06:00-06:59" 
                    break;
                    case 7:
                formatTime="07:00-07:59" 
                    break;
                    case 8:
                formatTime="08:00-08:59" 
                    break;
                    case 9:
                formatTime="09:00-09:59" 
                    break;
                    case 10:
                formatTime="10:00-10:59" 
                    break;
                    case 11:
                formatTime="11:00-11:59" 
                    break;
                    case 12:
                formatTime="12:00-12:59" 
                    break;
                    case 13:
                formatTime="13:00-13:59" 
                    break;
                    case 14:
                formatTime="14:00-14:59" 
                    break;
                    case 15:
                formatTime="15:00-15:59" 
                    break;
                    case 16:
                formatTime="16:00-16:59" 
                    break;
                    case 17:
                formatTime="17:00-17:59" 
                    break;
                    case 18:
                formatTime="18:00-18:59" 
                    break;
                    case 19:
                formatTime="19:00-19:59" 
                    break;
                    case 20:
                formatTime="20:00-20:59" 
                    break;
                    case 21:
                formatTime="21:00-21:59" 
                    break;
                    case 22:
                formatTime="22:00-22:59" 
                    break;
                    case 23:
                formatTime="23:00-23:59" 
                    break;
                default:
                formatTime="99:99:99~99:99:99:99"
                    break;
            }
        }
        if(flag=='year'){
            let date= new Date();
            switch (timeName) {
                case 1:
                 formatTime=date.getFullYear()+"-01"  
                    break;
                 case 2:
                 formatTime=date.getFullYear()+"-02"  
                    break;
                     case 3:
                 formatTime=date.getFullYear()+"-03"  
                    break;
                     case 4:
                 formatTime=date.getFullYear()+"-04"  
                    break;
                     case 5:
                 formatTime=date.getFullYear()+"-05"  
                    break;
                     case 6:
                 formatTime=date.getFullYear()+"-06"  
                    break;
                     case 7:
                 formatTime=date.getFullYear()+"-07"  
                    break;
                     case 8:
                 formatTime=date.getFullYear()+"-08"  
                    break;
                     case 9:
                 formatTime=date.getFullYear()+"-09"  
                    break;
                      case 10:
                 formatTime=date.getFullYear()+"-10"  
                    break;
                      case 11:
                 formatTime=date.getFullYear()+"-11"  
                    break;
                       case 12:
                 formatTime=date.getFullYear()+"-12"  
                    break;
                default:
                formatTime="9999-99-99"  
                    break;
            }
        }
        if(flag=='month'||flag=='years'){
         formatTime=timeName;   
        }
        return formatTime;
    }
    
  },
  mounted() {
    this.create('link');
    this.globalCount();
    this.globalAdmin();
    this.getPv();    
    this.getsource();
    this.chartPie = echarts.init(document.getElementById("chartPie"));
    this.chartPie.setOption(this.chartPieOptions);
    this.chartLine = echarts.init(document.getElementById("chartLine"));           
    this.chartLine.setOption(this.chartLineOptions);        
    window.addEventListener('resize', this.createChart);
    console.log('v9.3');
  },
 
};
</script>

<style lang="scss" scoped>
.gray-bg{
 
}
.span24 {
  margin-bottom: 24px;
}

.bg-box {
  background: #fff;
  height: 112px;
  display: flex;
  .bg-green {
    background: #17d57e;
  }
  .bg-yellow {
    background: #fec92b;
  }
  .bg-blue {
    background: #2da3fb;
  }
  .bg-purple {
    background: #c172d8;
  }
}

.bg-icon {
  text-align: center;
  padding-top: 22px;
  width: 35%;
  height: 100%;
  .iconfont {
    margin-top: 24px;
    font-size: 40px;
    color: #fff;
    text-align: center;
  }
  .icon-title {
    color: #fff;
    font-size: 14px;
    text-align: center;
    margin-top: 10px;
  }
}
.bg-info {
  width: 65%;
  padding: 24px;
}
.today-count {
  color: #5a5e66;
  font-size: 14px;
  .count-num {
    font-size: 18px;
    position: relative;
    top: 2px;
    margin-right: 4px;
    color: #353535;
  }
  .up-num {
    font-size: 14px;
    color: #ff724c;
  }
}
.all-count {
  font-size: 14px;
  color: #999;
  margin-top: 24px;
}
.h358 {
  height: 358px;
  background: #fff;
}
.h440 {
  height: 440px;
  background: #fff;
}
.work-header {
  height: 50px;
  line-height: 50px;
  padding: 0 16px 0 24px;
  display: flex;
  justify-content: space-between;
  .iconfont {
    font-size: 20px;
    color: #999999;
    &:hover {
      color: #353535;
    }
  }
}
.work-body {
  background: #fff;
  height: 308px;
  padding: 0 24px;
}
.index-table {
  width: 100%;
  th {
    color: #878d99;
    font-size: 12px;
    padding-bottom: 10px;
  }
  td {
    border-bottom: 1px dotted #e6ebf3;
    height: 32px;
    line-height: 32px;
    color: #5a5e66;
    font-size: 12px;
  }
  tr:last-child{
    td{ border-bottom: none;}
  }
}
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.systemInfo{
  font-size: 12px;
  color: #999;
  text-align: center;
  margin-top: 12px;
  margin-bottom:12px;

  span{
        margin-right: 14px;
  }
}
</style>

