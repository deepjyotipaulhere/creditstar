<template>
  <div>
	  <nav class="navbar navbar-light navbar-expand-lg fixed-top" id="mainNav">
        <div class="container">
			<a class="navbar-brand js-scroll-trigger" href="#page-top">CreditStar Repayment Calculator</a>
			<button data-toggle="collapse" data-target="#navbarResponsive" class="navbar-toggler float-right" aria-controls="navbarResponsive" aria-expanded="false"
                aria-label="Toggle navigation"><i class="fa fa-bars"></i>
			</button>
            <div class="collapse navbar-collapse" id="navbarResponsive">
            </div>
        </div>
    </nav>
    <header class="masthead" style="background:url('/img/bg-pattern.png'), linear-gradient(to left, #7b4397, #dc2430);height:100%;padding-top:100px">
        <div class="container h-100">
            <div class="row h-100">
                <div class="col-lg-6">
					<h3>Interest Rate: 25%</h3>
					<label>Loan Amount</label><input class="custom-range" type="range" step="100" min="100" max="1000" v-model="amount">
                    <h1 class="text-center" style="font-family: Muli, sans-serif;font-weight: 700;">&pound;{{amount}}</h1>
                    <div class="row">
                        <div class="col">
							<label>Period</label>
							<input class="custom-range" type="range" min="1" max="12" step="1" v-model="period">
							<h5 class="text-center">{{period}} Months</h5>
						</div>
                        <div class="col"><label>Monthly Repayment Date</label><input type="date" v-model="rdate"></div>
                    </div>
                </div>
                <div class="col-lg-6">
                    <h2>Total amount payable: <b>&pound;{{amount*1.25}}</b></h2>
                    <br>
                    <h4>Your Repayment Schedule</h4>
                    <div class="table-responsive">
                        <table class="table">
                            <thead>
                                <tr style="color:#fc0">
                                    <th>Payment Date</th>
                                    <th>Payable Amount(&pound;)</th>
                                    <th>Remaining Amount Payable(&pound;)</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(x,i) in getSchedule" :key="i">
                                    <td style="color:white">{{x.dt}}</td>
                                    <td style="color:#3f0;text-align:right"><b>{{x.amt}}</b></td>
                                    <td style="text-align:right;color:#96fbff">{{x.remaining}}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </header>
    <footer>
        <div class="container">
            <p>©&nbsp;CreditStar 2019. All Rights Reserved.</p>
            <ul class="list-inline">
                <li class="list-inline-item"><a href="#">Privacy</a></li>
                <li class="list-inline-item"><a href="#">Terms</a></li>
                <li class="list-inline-item"><a href="#">FAQ</a></li>
            </ul>
        </div>
    </footer>
  </div>
</template>

<script>
export default {
	head:{
		title: 'CrediStar Repayment Calculator',
		script:[
			{ src: '/js/jquery.min.js' },
			{ src: '/bootstrap/js/bootstrap.min.js' },
			{ src: 'https://cdnjs.cloudflare.com/ajax/libs/jquery-easing/1.4.1/jquery.easing.min.js' },
			{ src: '/js/new-age.js' },
		]
	},
	data(){
		return {
			amount:100,
			period:1,
			rdate:new Date().toLocaleDateString('en-GB')
		}
    },
    
    computed:{
        getSchedule(){
            var total=(this.amount*1.25).toFixed(2);
            var amtperperiod=(total/this.period).toFixed(2);
            var schedule=[];
            var p=new Date(this.rdate);
            for (let index = 0; index < this.period; index++) {
                total=Math.max(total-amtperperiod,0).toFixed(2)
                p.setMonth(p.getMonth()+1)
                schedule.push({'dt':new Date(p).toLocaleDateString('en-GB'), 'amt':amtperperiod, 'remaining':total})
            }
            return schedule
        }
    }
}
</script>

<style>
</style>
