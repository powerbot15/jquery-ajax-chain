jquery-ajax-chain
=================

Multiple ajax requests chaining with `jQuery.ajax()`
-------------------------------------------------

This is one of possible solutions for chaining ajax requests one by one. So each next request will start only when response of the previous request processed

      var counter = 0,
          requestsCount = 100,
          chainedResponses = [];
      (function chain(url){
        $.get(url)
          .done(function(response){
            counter++;
            chainedResponses.push(response); //current response saved
            if(counter < requestsCount){ //
                chain('/page' + counter); // now recursion !
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
      })('/page0');     //the first request url
