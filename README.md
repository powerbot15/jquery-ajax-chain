jquery-ajax-chain
=================

Multiple ajax calls chaining

      var counter = 0,
          requestsCount = 100,
          chainedResponses = [];
      (function chain(url){
        $.get(url)
          .done(function(response){
            counter++;
            chainedResponses.push(response);
            if(counter < requestsCount){ //
                chain('/page' + counter);
            }
            else{
              console.dir(chainedResponses); //all data accepted from all calls now proceed it
            }
          })
          .fail(function(error){
            chainedResponses.push(false);
            counter++;
            if(counter < requestsCount){
              chain('/page' + counter);  //if error we need continue the chain to the end
            }
            else{
              console.dir(chainedResponses); //all data accepted from all calls now proceed it
            }
          })
      })('/page0');
