var com_ops={
    init:function () {
        this.eventBind();
    },

    eventBind:function () {
        //返回顶部
        $(".back_top_div").click(function () {
            $('body,html').animate({
                scrollTop:0
            },300)
        });

        $(window).scroll(function () {
            if($(window).scrollTop()>400){
                $(".back_top_div").css('display','block');
                $(".detail-nav").css('display','block');
            }else{
                $(".back_top_div").css('display','none');
                $(".detail-nav").css('display','none');
            }
        });


        //微信弹出层
        $("#layer_weixin").click(function () {
            $("#layer-mask").show();
            $("#layer-pop").show();
            $("#layer-close").click(function () {
                $("#layer-mask").hide();
                $("#layer-pop").hide();
            });
        });

        //qq弹出层
        $("#layer_qq").click(function () {
            $("#layer-mask1").show();
            $("#layer-pop1").show();
            $("#layer-close1").click(function () {
                $("#layer-mask1").hide();
                $("#layer-pop1").hide();
            });
        });

        //热点问题、使用技巧和fqa详情页
        $('.hotdi>span').click(function(ev){
            var ulCode=$(this).next('ul');
            ulCode.slideToggle();
            $(this).children('.fa-chevron-circle-down').toggleClass('hidden');
            $(this).children('.fa-arrow-circle-up').toggleClass('hidden');
        });

        $('.itemList>li').click(function () {
            $('#itemList>li').css({
                color:'#000',
                backgroundColor:'#fff'
            })

            $(this).css({
                color:'red',
                backgroundColor:'#fff'
            })
        });

        //轮播图
        window.onload = function () {
            var bannerH = $('#item_banner img:visible').height();
            $('.layui-carousel').css('height',bannerH+'px');
        }
        window.onresize = function () {
            var bannerH = $('#item_banner img:visible').height();
            $('.layui-carousel').css('height',bannerH+'px');
        }
        layui.use('carousel', function(){
            var carousel = layui.carousel;
            //建造实例
            carousel.render({
                elem: '#test1'
//            ,height:'750'
                ,width: '100%' //设置容器宽度
                ,anim: 'fade' //切换动画方式
                ,arrow:'hover'
                ,interval:4000
            });
        });

        //保修查询
        $("#keepBtn").click(function () {
            var code=$('#keepCode').val();
            if(!code){
                alert('请先输入产品序列号！')
                return;
            }
            $('.keepResult').html('正在查询中...');
            url=SCOPE.code_url;
            postData={'code':code};
            $.post(url,postData,function (result) {
                if(result.data.code == code){
                    data=result.data;
                    code_html='';
                    code_html='<p>购买机型：<span>'+data.type+'</span></p>\n' +
                        '                <p>出厂日期：<span>'+data.time+'</span></p>\n' +
                        '                <p>保修截止：<span>'+data.baoxiu+'</span></p>\n' +
                        '                <p>配&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;置：<span>'+data.node+'</span></p>'
                    $('.keepResult').html(code_html);
                }else{
                    $('.keepResult').html('请检查输入的序列号是否正确!').css('color','red');
                }
            },'json')
        });


        //省份
        $('#provinces').change(function(){
            var province_id=$(this).val();
            $.ajax({
                url:common_ops.WebUrl('/api/search/provinces'),
                type:'POST',
                data:{id:province_id},
                dataType:'json',
                success:function( res ){
                    var data = res.data;
                    $("#citys").html("");
                    $("#citys").append("<option value='0'>请选择市级</option>");
                    for(var i = 1;i<data.length;i++){
                        $("#citys").append("<option value='"+data[i].city_id+"'>"+data[i].city+"</option>");
                    }
                }
            });
        });

        //市级
        $('#citys').change(function(){
            var city_id=$(this).val();
            url = common_ops.WebUrl('/api/search/citys');
            postData={'id':city_id};
            $.post(url,postData,function (result) {
                if(result.status==1){
                    data=result.data;
                    city_html='';
                    $(data).each(function () {
                        city_html += "  <table class=\"table\">\n" +
                            "                <tbody>\n" +
                            "                <tr class=\"active service_table_tr\">\n" +
                            "                    <td style='width: 50%'>\n" +
                            "                        <span class=\"glyphicon glyphicon-map-marker\"></span>\n" +
                            "                        <div class=\"address_a\">"+this.server+"</div>\n" +
                            "                        <div class=\"address_b\">"+this.address+"</div>\n" +
                            "                    </td>\n" +
                            "                    <td style='width: 25%'><span style='font-weight: bold'>联系人</span><br><br>"+this.contact+"</td>\n" +
                            "                    <td style='width: 25%'><span style='font-weight: bold'>联系方式</span><br><br>"+this.iphone+"<br>"+this.tell+"</td>\n" +
                            "                </tr>\n" +
                            "                </tbody>\n" +
                            "            </table>"
                    });
                    $('.service_custom').html("<h3>客户服务中心:</h3>");
                    $('.service-row').html(city_html);
                }else if(result.status == 0){
                    $('.service-row').html(" ");
                    layer.msg(result.data);
                }
            },'json')

        });

    }
};

$(function () {
    com_ops.init();
});
