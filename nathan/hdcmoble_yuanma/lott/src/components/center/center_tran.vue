<template lang="jade">
.transform
 .ctranT
  icon(name="database",style="top:0.05rem")
  | 中心钱包
  span(style="margin-left:0.6rem;") 余额 :
   span(style="margin-left:0.25rem;") {{$store.state.register.amountmoney}}
   |  元
  v-touch.ctraf(tag="span",@tap="$store.commit('chauser','showTip')")
   icon(style="width:0.4rem;height:0.4rem",name="refresh")
 .ccontent
  .t_title
   .from 从
    select(v-model="cout")
     option(value="ms") [主账户]
     option(value="ag") [AG平台]
     option(value="bb") [BBIN平台]
     option(value="pt") [PT平台]
     option(value="mg") [MG平台]
     option(value="sa") [SA平台]
     option(value="gg") [GG平台]
     option(value='ww') [ww平台]
     option(value='nn') [牛牛彩平台]
   .to 到
    select(v-model="cin")
     option(value="ag") [AG平台]
     option(value="bb") [BBIN平台]
     option(value="pt") [PT平台]
     option(value="mg") [MG平台]
     option(value="sa") [SA平台]
     option(value="gg") [GG平台]
     option(value='ww') [ww平台]
     option(value='nn') [牛牛彩平台]
     option(value="ms") [主账户]
  .t_choice
   ul
    li(v-for="(item,$index) in $store.state.register.choices")
     p {{item.text}}
     p
      span 转出|
      span 转入
     p {{item.eachMoney}}
     p
      v-touch(tag="span",@tap="getEachMoney($index)")
       icon(name="refresh")
  input.t_input(style="width:10rem;margin:0 auto;margin-bottom:0.6rem;",v-model="$store.state.register.tranforMoney",placeholder="请输入转账金额",type="text")
 v-touch(tag="button",@tap="transform",class="t_btn") 开始转账
</template>
<script>
	export default{
    data(){
      return{
        cin_ms:false,
        cin_rest:true,
        cout:'ms',
        cin:'ag'
      }
    },
    watch:{
        cout:function(){
          this.$store.state.register.cout=this.cout;
          if(this.cout!=='ms'){
             this.cin='ms';
          }else{
            this.cin='ag';
          }
       },
       cin:function(){
        this.$store.state.register.cin=this.cin;
        if(this.cin!=='ms'){
          this.cout='ms';
        }else{
          this.cout='ag';
        }
       }
     },
	   mounted:function(){
	   	if(this.$store.state.register.loginStatus!==null){
	   		for(let i = 0;i<this.$store.state.register.choices.length;i++){
	   	    this.$store.dispatch("getEachMoney",{num:i,m:'c'});
	   	    }
	   	}
	   },
	   methods:{
	   	 getEachMoney($index){
	   	 	this.$store.dispatch("getEachMoney",{num:$index,m:'c'});
	   	  },
	   	  transform(){
	   	  	this.$store.dispatch("tranformMoney");
	   	  },
	   }
	}
</script>
<style lang="scss">
	@import '../../assets/css/main.scss';
  .transform{
    width:rem2px(750);
    margin:0 auto;
  }
	.ctranT{
    @extend %font26;
    @extend %bz;
    background-color:#fff;
    padding-top:rem2px(30);
    padding-left:rem2px(55);
    height:rem2px(90);
    text-align:left;
    color:#858585;
    svg{
     @extend %posr;
     width: rem2px(32);
     height: rem2px(32);
     top: 0.105rem;
     margin-right:rem2px(30);
    }
	}
	.ctraf{
		margin-left:0.65rem;
		display:inline-block;
		svg{
			width:0.30rem;
			height:0.30rem;
      border-radius:0.08rem;
      padding:0.10rem;
      border:1px solid #858585;
		}
	}
	.ccontent{
    @extend %font25;
		background-color:#fff;
		margin-top:rem2px(50);
		padding-top:rem2px(25);
		@extend %bz;
		border:{
			top:2px solid $bc;
			bottom:2px solid $bc;
		}
	}
	.t_title{
		>div{
			@extend %fl;
      @extend %font26;
		}
		.from{
      color:#5478b3;
      margin-left:rem2px(60);
      margin-bottom:rem2px(25);
			select{
		      @extend %bz;
          @extend %font24;
          color:#5478b3 ;
          margin-left:rem2px(10);
  				padding-left:rem2px(10);
          width:rem2px(200);
          height:rem2px(38);
          border:1px solid #5478b3;
			}
		}
		.to{
			margin-left:rem2px(50);
			color:#ff9000;
			select{
			  @extend %font24;
				margin-left:rem2px(10);
				padding-left:rem2px(10);
        color:#5478b3;
        width:rem2px(200);
        height:rem2px(38);
				color:#ff9000;
				border:1px solid #ff9000;
			}
		}
	}
	.t_choice{
		border-top:1px solid $bc;
		clear:both;
		padding-top:0.2125rem;
		padding-left:0.9375rem;
		color:#737373;
		margin-top:1.0rem;
		@extend %bz;
    @extend %font24;
		li{
      width:85%;
			height:rem2px(75);
      line-height:rem2px(75);
		}
		p{
			@extend %fl;
		}
		p:first-child{
			width:3.5rem;
			text-align:left;
		}
		p:nth-child(2){
			margin-right:rem2px(120);
		}
		p:last-child{
      @extend %fr;
			span:last-child{
				display:block;
        margin-right:0.2rem;
          svg{
            border:1px solid #000;
            padding:rem2px(5);
          	color:#000;
            width:rem2px(16);
            height:rem2px(16);
            border-radius:0.05rem;
          }
			}
		}
	}
</style>
