(function(rendezvous){
    var parallelProcesses = [];
    var rendezvousProcess = null;
    var breakOnError = false;
    var resultCollection = {};
    resultCollection.count = 0;


    rendezvous.execute = function(args){

        parallelProcesses = args.parallelProcesses;
        rendezvousProcess = args.rendezvousProcess;
        breakOnError = args.breakOnError || false;
        resultCollection = {};
        resultCollection.count = 0;

        parallelProcesses.forEach(function(process){

            rendezvous.executeParallelProcesses(process);

        });
    };

    rendezvous.executeParallelProcesses = function(process){
        process.execute(function(err, result){

            resultCollection[process.name] = {
                'error': err,
                'result': result
            };

            resultCollection.count += 1;
            if(parallelProcesses.length === resultCollection.count
            || breakOnError && err){

                rendezvousProcess(resultCollection);
            }
        });

    };

}(module.exports));
