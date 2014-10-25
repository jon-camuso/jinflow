jinflow
=======

JavaScript Workflow Library


A JavaScript library of control-flow pattern implementations


## Usage

    var rendezvous = require('../jinflow').rendezvous;

    // data object needs to make two asynchronous database calls to 
    // obtain all of the model information.
    // rendezvous' execute method is passed an object containing an array 
    // of "parallel processes" objects that have names and functions and 
    // a rendezvous process.
    // The rendezvous process "callback" will only be executed when both
    // parallel process' execute functions have completed.
    //
    data.getHome = function(callback){

        rendezvous.execute({
            parallelProcesses:[
                {
                    'name':'document',
                    'execute':function(activityCallback){
                        data.getDocument({'path': '/'}, activityCallback);
                    }
                },
                {
                    'name':'responses',
                    'execute':function(activityCallback){
                        data.getResponses({'path' : '/'}, activityCallback);
                    }
                }
            ],
            rendezvousProcess:callback
        });
    };
