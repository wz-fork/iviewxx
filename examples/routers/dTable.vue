<template>
    <div>
        <div style="margin-top:10px">
            <dTable highlight-row border :context="self" :columns="columns8" :data="data7"></dTable>
            <Page :total="total" :page-size="pageSize" :current="pageNo" size="small" show-total @on-change="changePage"></Page>
        </div>
        <div style="margin-top:10px">
            <Button @click="addColumn">增加一列</Button>
        </div>
    </div>
</template>
<script>
    import abc from '../components/test.vue';
    export default {
        components: { abc },
        data () {
            return {
                self: this,
                pageSize: 3,
                total: 3,
                pageNo: 1,
                data8: [
                    {
                        orderNum:"54465456456",
                        buyer:"大王0xx",
                        country:"中国122",
                        pay:"支付宝",
                        status:"未处理",
                        sex: 'male',
                        stretch:true,//是否显示子菜单
                        children:[
                            {
                                orderNum:"324234",
                                buyer:"大王00",
                                country:"中国2",
                                pay:"支付宝",
                                status:"未处理",
                                indentSize:15,//自定义的间距
                                stretch:false,
                                sex: 'male',
                                children:[
                                    {
                                        orderNum:"123123",
                                        buyer:"大王000",
                                        country:"中国3",
                                        pay:"支付宝",
                                        status:"未处理",
                                        indentSize:30,
                                        stretch:false,
                                        sex: 'male',
                                        children: [
                                            {
                                                orderNum:"xxxaaa",
                                                buyer:"大王03300",
                                                country:"中国cdc3",
                                                pay:"支付宝",
                                                status:"未处理",
                                                indentSize:40,
                                                sex: 'male',
                                                stretch:false
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                orderNum:"gggg666",
                                buyer:"大王01",
                                country:"中国4",
                                pay:"支付宝",
                                status:"未处理",
                                indentSize:15,
                                sex: 'male',
                                stretch:false
                            },
                            {
                                orderNum:"43",
                                buyer:"大王02",
                                country:"中国1",
                                pay:"支付宝1",
                                status:"未处理",
                                sex: 'male',
                                indentSize:15,
                                stretch:false
                            },
                            {
                                orderNum:"43",
                                buyer:"大王03",
                                country:"中国",
                                pay:"支付宝",
                                status:"未处理",
                                sex: 'male',
                                indentSize:15,
                                stretch:false
                            },
                            {
                                orderNum:"956599555",
                                buyer:"大王04",
                                country:"中国1",
                                pay:"支付宝1",
                                status:"未处理",
                                sex: 'male',
                                indentSize:15,
                                stretch:false
                            },
                            {
                                orderNum:"5656",
                                buyer:"大王05",
                                country:"中国",
                                pay:"支付宝",
                                status:"未处理",
                                sex: 'male',
                                indentSize:15,
                                stretch:false
                            },
                            {
                                orderNum:"656556",
                                buyer:"大王06",
                                country:"中国1",
                                pay:"支付宝1",
                                status:"未处理",
                                sex: 'male',
                                indentSize:15,
                                stretch:false
                            }
                        ]
                    },
                    {
                        orderNum:"x11",
                        buyer:"大王1",
                        country:"中国",
                        pay:"支付宝",
                        status:"未处理",
                        sex: 'male',
                        stretch:false
                    },
                    {
                        orderNum:"456456456",
                        buyer:"大王2",
                        country:"中国",
                        pay:"支付宝",
                        status:"未处理",
                        sex: 'male',
                        stretch:false,
                        children:[
                            {
                                orderNum:"222",
                                buyer:"大王20",
                                country:"中国",
                                pay:"支付宝",
                                status:"未处理",
                                sex: 'male',
                                indentSize:15,
                                stretch:false,

                            }
                        ]
                    }
                ],
                data7: [],
                columns8:[
                    {
                        type: 'selection',
                        width: 70,
                        align: 'center'

                    },
                    {
                        type: 'switch',
                        title: '订单号',
                        key: 'orderNum',
                        minWidth:700
                    },
                    {
                        title: '买家',
                        key: 'buyer',
                        combine:true,
                        render:(h,params)=>{

                            const obj = {
                              childrens:[["div",{class:"combiePackageCode"},321],['div',{class:"combineShipping"},'123 > 321'],['span',{class:"icon iconfont icon-dayin prinTime"},'']],
                              props: {
                              },
                            };
                            if (params.index === 1) {
                                 obj.props.colSpan = 3;

                            }
                            return obj;
                        }
                    },
                    {
                        title: '国家',
                        key: 'country',
                        combine:true,
                        width: 200,
                        render : (h,params) =>{
                            const obj = {
                              childrens:  params.row.country,
                              props: {},
                            };
                            if (params.index === 3) {
                              obj.props.rowSpan = 2;
                            }
                            // These two are merged into above cell
                            if (params.index === 7) {
                              obj.props.rowSpan = 2;
                            }
                           /* if (params.index === 7) {
                              obj.props.colSpan = 4;
                            }*/
                            return obj;

                        }
                    },
                    {
                        title: '付款',
                        key: 'pay'
                    },
                    {
                        title: '状态',
                        key: 'status'
                    },
                    {
                        title: '标记',
                        key: 'action',
                        width: 180,
                        align: 'center',
                        render (h,params) {
                           return h('Button',{
                           },"编辑")
                        }
                    }
                ]
            }
        },
        methods: {
            remove (index) {
                this.data6.splice(index, 1);
            },
            show () {
                this.modal9 = true;
            },
            changePage (page) {
                this.pageNo = page;
                this.data7 = [this.data8[page - 1]];
            },
            addColumn () {
                let col = {
                    key: 'sex',
                    title: '性别',
                    width: 100
                }
                this.columns8.splice(4, 0, col);
            }
        },
        mounted (){
            var self = this;
            this.data7 = this.data8;
        }
    }
</script>