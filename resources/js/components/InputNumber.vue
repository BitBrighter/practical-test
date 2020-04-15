<template>
    <div class="flex-center position-ref full-height">
        <div class="content">
            <div class="container">

                <div class='backbutton'><a href="../" class="btn btn-primary">&lsaquo; Back</a></div>

                <div class="row">
                    <div class="col-md-12 justify-content-center">

                        <form id="inputform" @submit='checkForm' action="#" method="POST">
                        
                            <div class='card'>
                                <div class='card-header'>Input Form</div>
                                <div class='card-body'>
                                    
                                        <div class="form-group">
                                            <label for="numberinput">Enter a number between 1 and 100</label>
                                            <input type="number" min="1" max="100" class="form-control" v-model="fields.name" id="numberinput" placeholder="1 - 100" required>
                                        </div>
                                                                
                                    </div>
                                <div class='card-footer'><button type="submit" class="btn btn-primary">Submit</button></div>                    
                            </div>

                        </form>

                        <transition name="fade"><div v-if="omittedShow" class="omittedShow"><strong>Omitted Value:</strong> {{ this.omittedValue }}</div></transition>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.');
        },
        data: function(){
            return {
                fields: {},
                arrayMin: 1,
                arrayMax: 100,
                omittedValue: '',
                omittedShow: false
            }
        },
        methods: {
            findMissingNumber: function( numarr ){
                var omitted = false;
                for(var i=this.arrayMin; i<this.arrayMax; i++){
                    if(numarr.indexOf(i) == -1) {
                        omitted = i;
                    }                       
                }              
                return omitted;
            },
            checkForm: function (e) {
                e.preventDefault();

                var numberarray = [];
                for(var i=this.arrayMin; i<this.arrayMax; i++){
                    if(i != this.fields.name){
                        numberarray.push(i);
                    }
                }

                this.omittedValue = this.findMissingNumber(numberarray);
                this.omittedShow = true;
            }
        }
    }
</script>

<style>
    .full-height {
        height: 100vh;
    }

    .flex-center {
        align-items: center;
        display: flex;
        justify-content: center;
    }

    .position-ref {
        position: relative;
    }

    .top-right {
        position: absolute;
        right: 10px;
        top: 18px;
    }

    .content {
        text-align: center;
    }

    .backbutton{ text-align:left; padding-bottom:30px; }
    
    .omittedShow{ padding:30px 0; }
    
    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }

    .fade-enter, .fade-leave-to {
        opacity: 0;
    }

</style>

