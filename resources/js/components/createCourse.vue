<template>
	<div class="m-0 p-0">
		
	<div class="row bg-light m-0 px-2 pt-4">
            <div class="col-lg-3 col-md-5 col-sm-12 m-0 ">
            	<p class="fs2 fw8 font">Create Course</p>
            	<div  class="w-100 bg-white r2 px-4 py-4 shadow-sm"><!-- loop weekly -->
						<div class="d-flex flex-wrap-center mb-4" >
							<span class="ncircle" v-bind:class="{tactive:stageone,tsuccess:stageonep}" >1</span>
							<span class="tline" v-bind:class="{tlactive:stageone,tlsuccess:stageonep}"></span>
							<div class="fs1 w10 no-break ml-3">Course Details </div>						
						</div>
						<div class="d-flex flex-wrap-center mb-4 ">	
							<span class="ncircle" v-bind:class="{tactive:stagetwo,tsuccess:stagetwop}">2</span>
							<span class="tline" v-bind:class="{tlactive:stagetwo,tlsuccess:stagetwop}"></span>
							<div class="fs1 w10 no-break ml-3">Add Experiment</div>							
						</div>
						<div class="d-flex flex-wrap-center mb-4 ">	
							<span class="ncircle"  v-bind:class="{tactive:stagethree,tsuccess:stagethreep}">3</span>
							<span class="tline" v-bind:class="{tlactive:stagethree,tlsuccess:stagethreep}"></span>
							<div class="fs1 w10 no-break ml-3">Add Resources</div>
						</div>
						<div class="d-flex flex-wrap-center mb-4 ">	
							<span class="ncircle"  v-bind:class="{tactive:stagefour,tsuccess:stagefourp}">4</span>							
							<div class="fs1 w10 no-break ml-3">Add Instruction</div>
						</div>
				</div>
            			   	
            </div>
            	
            <div class="col-lg-8 col-md-7 col-sm-12 pt-3" style="height: 550px;">
            	<!-- course detatil -->            	
            	<div  class="py-4 px-4 mt-3 r2 bg-white shadow-sm" style="">
            		<div id="cdetail" v-if="sectionState==1" class="m-0 p-0">            			
	            		<p class="fw8 fs1 font" style="color: #777;">Course Details</p>
	            		<div class="row">            			
	            			<div class="col-lg-8 col-md-6 m-0">
	            				<p class="fs001 my-1">Course Title</p>
	            				<input type="text" @keyup="normalize" class="form-control vI" id="ctitle">
	            			</div>
	            			<div class="col-lg-1 col-md-1 m-0 px-0"></div>
	            			<div class="col-lg-3 col-md-5 m-0">
	            				<p class="fs001 my-1">Course Code</p>
	            				<input type="text"  @keyup="normalize" class="form-control vI" id="ccode">
	            			</div>
	            			<div class="col-lg-12 col-md-12 mt-3">
	            				<p class="fs001 my-1">Course Code</p>            				
	            				<textarea @keyup="normalize" class="form-control vI" rows="6" id="cdescription"></textarea>
	            			</div>
	            		</div>
	            	</div>
	            	<div id="addExperiment" v-if="sectionState==2" class="m-0 p-0 shineA">     
	            			<p class="fw8 fs1 font" style="color: #777;">Add Experiment</p>
	            			<div class="row">            			
		            			<div class="col-lg-8 col-md-6 m-0">
		            				<p class="fs001 my-1">Select Experiment</p>
		            				<div class="d-flex">
		            					<select @keyup="normalize" class="form-control vI" id="selectExperiment">
		            						<option></option>
		            						<option value="1">Vernier Caliper</option>
		            						<option value="3">Micrometer Screw Guage</option>
		            						<option value="2">Simple Pendulum</option>
		            					</select>
		            					<button class=" ml-2 sysbtn p-success text-white" @click="addEBox">Add</button>
		            				</div>
		            				<br><br>
		            				<div class="d-flex flex-wrap-center justify-content-between w-100">
		            					<div class="hr w35"></div>
		            					<span class="w30">Added Experiment</span>
		            					<div class="hr w35"></div>
		            				</div>
		            				<br>
		            				<div id="addEBox" class="r1" style="height: 200px;">
		            					
		            				</div>
		            			</div>
	            			</div>       			
	            	</div>
            	</div>
            	
            	{{alldata}}         
            	{{selectedExperiment}}
            </div> 
   		</div>
        <div class="row bg-white m-0">
            <div class="col-lg-8 col-md-7 col-sm-12">
            </div>
            <div class="col-lg-2 col-md-3 col-sm-12 mx-auto py-2 d-flex">
            	<button v-if="sectionState >1" class="btn p-success text-white py-2 px-3 mr-3" @click="nextSection" ><span class="fa fa-arrow-left"></span> Previous </button>
            	<button class="btn p-success text-white py-2 px-3" @click="nextSection" > Continue <span class="fa fa-arrow-right"></span></button>
            </div>
            <div class="col-lg-2 col-md-1 col-sm-12 mx-auto">
            </div>
        </div>
	</div>
</template>

<script>
	export default{

	 data:function() {
	    	return{
	    	 alldata:[],
	    	 stageone:true,
	    	 stageonep:false,
	    	 stagetwo:false,
	    	 stagetwop:false,
	    	 stagethree:false,
	    	 stagethreep:false,
	    	 stagefour:false,
	    	 stagefourp:false,
	    	 navState:false,
	    	 courseTrend: 4,
	    	 sectionState: 1,
	    	 title:'',
	    	 ccode:'',
	    	 validateState:false,
	    	 selectedExperiment:[],
	    	 selectedExperimentName:[]
	    	}
        },
        methods:{
        	toggleExperimentGuider: function () {
//        		alert(this.navState);
        		this.navState = !this.navState;
			   this.$eventBus.$emit('toggleClick',{text:this.navState});
			    //this.newTodoText = ''
			},
			
			addEBox:function(){
				let obj = $('#selectExperiment');
				let evalue = Number(obj.val());
				this.validateState =false;

				if($('#selectExperiment option:selected').text()!=""){
					this.validateState =true;
					let selExpName = $('#selectExperiment option:selected').text();
					if(!this.selectedExperiment.includes(evalue)){
					  this.selectedExperiment.push(evalue);
					  this.selectedExperimentName.push(selExpName);
					  let $vm = this;
					///alert(this.selectedExperiment.includes(evalue));
					 let indexof = this.selectedExperiment.indexOf(evalue);
						$('#addEBox').append("<div class='d-flex justify-content-between flex-wrap-center' style='font-size:0.9em;' id='"+this.selectedExperiment.indexOf(evalue)+"'><p class='py-2 pl-3 my-0'><b >Experiment "+(Number(this.selectedExperiment.indexOf(evalue))+1)+'</b>:<span class="ml-5"></span> '+selExpName+"</p> <span class=' mt-2 close d-flex justify-content-around flex-wrap-center rmexp' style='background:#ccc; border-radius:50%;width:25px;height:25px;' rel='"+indexof+"' >&times</span></div><hr>")
					}else{
						$('#ar000').remove();
					   $('#addEBox').after('<span class="text-danger requiredv" id="ar000">already exist!</span>');				
					}
					
				}else{
					obj.after('<span class="text-danger requiredv">Required !</span>');	
					obj.css('border','1px solid #e45');
				}			
			},
			reiterateSelectedExp(){
				$('#addEBox').html("");
				for (let i = 0; i < this.selectedExperiment.length; i++) {
					$('#addEBox').append("<div class='d-flex justify-content-between flex-wrap-center' style='font-size:0.9em;' id='"+i+"'><p class='py-2 pl-3 my-0'><b >Experiment "+(i+1)+'</b>:<span class="ml-5"></span> '+this.selectedExperimentName[i]+"</p> <span class=' mt-2 close d-flex justify-content-around flex-wrap-center rmexp' style='background:#ccc; border-radius:50%;width:25px;height:25px;' rel='"+i+"' >&times</span></div><hr>")	
					}
			},
			singleValidate: function(id){
				$('#'+id).css('border','1px solid #e45');
				$('.requiredv').remove();
				$('#'+id).after('<span class="text-danger requiredv">Required !</span>')
			},
			validateI: function(id,sel=0){
				if (sel ===0) {

					let index =-1;
					$('#'+id).find('.vI').each(function(){
						index++;
					});
					let $vm = this;
					$('#'+id).find('.vI').each(function(e){
						if($(this).val()==""){
							$(this).css('border','1px solid #e45');
							$('.requiredv').remove();
							$(this).after('<span class="text-danger requiredv">Required !</span>');						
							$vm.validateState = false;
							return false;
						}					
						if(e == index){
							$vm.validateState = true;
						}
					})
				}
				if (sel=== 1) {
					if($('#'+id+ 'option:selected').text()==""){
						$('#'+id).css('border','1px solid #e45');
						$('.requiredv').remove();
						$('#'+id).after('<span class="text-danger requiredv">Required !</span>');						
						this.validateState = false;
						alert(1)
					}else{
						alert(2)

						this.validateState = true;	
					}
				}
			},

			//turn input back normal
			normalize:function(el){
				el.target.style.border = "1px solid #eee";
				$('.requiredv').remove();
			},
			nextSection: function(){
				if (this.sectionState === 1){	
					this.validateI('cdetail');
					
					if(this.validateState === true){
						this.ctitle = $('#ctitle').val();
						this.alldata.push({title: $('#ctitle').val(),ccode:$('#ccode').val(),cdescription:$('#cdescription').val()});
						this.sectionState = 2;						
						this.stageone= false;
				    	this.stageonep = true;
				    	this.stagetwo = true;
					}
				
				}else if (this.sectionState === 2){
					if (this.selectedExperiment.length == 0){
					 this.singleValidate('addEBox');
					}else{
						this.stagetwo= false;
				    	this.stagetwop = true;
				    	this.stagethree = true;
				    	this.sectionState = 3;
					}

				}
			}
        },	

        
         props: [],
         mounted: function () {
		  this.$nextTick(function () {
		    // Code that will run only after the
		    // entire view has been rendered
         	var $vm = this;
         		$(document).on('click', '.rmexp', function() {					
					$vm.selectedExperiment.splice($(this).attr('rel'),1);
					$vm.selectedExperimentName.splice($(this).attr('rel'),1);
         			$vm.reiterateSelectedExp();
         			/*
					$('#'+$(this).attr('rel')).remove();					
					*/
				});
		  })
		},
         events :{
         	'toggleClick':'toggleClick'
         }

	}
</script>
<style scoped>
	.close{
		background: #ccc !important;
		border-radius: 50% !important;
		padding: 2px !important;
	}
	.form-control:focus{
		outline: none !important;
		box-shadow: none !important;
		border: 1px solid #aaa;
	}
	.bb{
		border-bottom: 1px solid #ccc !important;
	}
	.requiredI{
		transition: all 1s;
		color: #e45 !important;
		background: white;
		border: 1px solid #aaa;
		box-shadow: 1px 2px 3px #bbb;
		border-radius: 5px;
		padding: 4px;
		display: block;
		position: absolute;
		top: 10px; /* At the bottom of the tooltip */
	  	left: 50px;
	  	z-index: 15;
	}
	.requiredI:before {
	  content: " ";
	  position: relative;
	  top: 0%; /* At the bottom of the tooltip */
	  left: 50%;
	  margin-left: -5px;
	  border-width: 5px;
	  border-style: solid;
	  border-color: black transparent transparent transparent;
	}
	.sysbtn{
		 padding: 10px 15px;
		  font-family: 'Roboto',serif;
		  font-size: 0.9em;
		  text-align: center;
		  text-decoration: none;
		  border-radius: 6px;
		  word-break: keep-all;
		  white-space: nowrap;
		  border: none;
		  position: relative;
	}
	.sysbtn:active{
		box-shadow: 0px 2px 0px 0px rgba(0,0,0,.2);
  		top: 1px;
	}
	.sysbtn:focus{
		box-shadow: inset 0 2px 3px #294,
	}
	.ncircle{
		border: 2px solid #bbb; 
		border-radius: 50%;
		width: 25px;
		height: 25px;
		font-size: 0.9em;
		padding: 2px 0px 0px 6.5px !important;
		transition: all 1s;
	}
	div{
		font-family: 'Roboto', sans-serif;
	}
	.no-break{
		white-space: nowrap;
		word-break:keep-all;
	}
	.tline{
		height: 27px; width: 2px; background: #bbb; position: relative; top:26px; left: -13px;
	}
	@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap');
	.syscircle{
		width: 12px !important;
		height: 12px !important;
		border-radius: 50%;
		background: #00b96b;
		display: block;
		margin: 0px 0px 0px 12px;
	}
	.tactive{
		border:2px solid #222 !important;
	}
	.tlactive{
		background: #222 !important;
	}
	.tsuccess{
		border: 2.5px solid #4b6 !important;
		background: #4b6 !important;
		color:white;
		padding-bottom: 2px;
	}
	.tlsuccess{
		background: #4b6 !important;
	}
	.syscircle-o{
		width: 12px;
		height: 12px;
		border-radius: 50%;
		border: 2px solid #999;
		display: block;	
		margin-left:12px;
	}
	.syscircle-o-l{
		width: 22px;
		height: 22px;
		border-radius: 50%;
		border: 2px solid #999;
		display: block;	
		margin-left: 5px;
	}
	.fs3{
		font-size: 1.7em;
	}
	.fs1{
		font-family: 'Roboto', sans-serif;
		font-size: 0.9em;
		color: #888;
		font-weight: 300;
	}
	.flex-wrap-center{
		flex-wrap: wrap;
		align-items: center;
	}
	.w10{
		width: 60px;
	}
	.timelineX{
		margin-top: 10px; 
		margin-bottom: 120px; 
	}
	.timelineX-o{
		margin-top: 10px; 
		margin-bottom: 120px; 
	}
	.timelineSM:before{
		content: "";
		height: 40px;
		width: 2px;
		background: #00b96b;		
		display: block;
		position: relative;
		top: 31px;		
		left: 77px;
	}
	.timelineSM-o:before{
		content: "";
		height: 40px;
		width: 2px;
		background: #999;		
		display: block;
		position: relative;
		top: 31px;		
		left: 77px;
	}
	.timelineX-o:before{
		content: "";
		height: 140px;
		width: 2px;
		background: #999;		
		display: block;
		position: relative;
		top: 31px;		
		left: 77px;
	}
	.timelineX:before{
		content: "";
		height: 132px;
		width: 2px;
		background: #00b96b;		
		display: block;
		position: relative;
		top: 10px;		
		left: 5px;
	}
	.timelineX-o:before{
		content: "";
		height: 130px;
		width: 2px;
		background: #999;		
		display: block;
		position: relative;
		top: 10px;		
		left: 3px;
	}
	.fw8{
		font-weight: 600;
		color: #222;
	}
	.fw3{
		font-weight: 600 !important;
		color: #222 !important;
	}
	.fs001{
		font-size: 0.8em;
		color: #888;
	}
	.fs2{
		font-size: 1.2em;
	}
	.wrap-center{
		  flex-wrap: wrap;
      align-items: center;
	}
	.hr{
		height: 1px !important;
		background: #ccc;
		width: 100% !important;
		display: block !important;
	}
	.w35{
		width: 35% !important;
	}
	.w30{
		width: 30%;
	}
	.shineA{
		transition: all 1s;
	}
</style>