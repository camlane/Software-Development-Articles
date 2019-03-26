# Software-Development-Articles<br />
A collection of the best of the best articles<br/>

Testing
Excellent advice on end to end testing<br />
https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html<br />

Junit testing best practices<br/>
https://blog.codecentric.de/en/2016/01/writing-better-tests-junit/

Coding
The definitive guide to Java 8 streams<br/>
http://winterbe.com/posts/2014/07/31/java8-stream-tutorial-examples/<br/>

Excellent summary of how a reactive stream works<br/>
https://opencredo.com/reactive-event-processing-reactor-core-first-look/<br/>

REST
HTTP error codes (with those pertaining to rest highlighted)<br />
https://blog.restcase.com/rest-api-error-codes-101/<br />

REST with Spring - A great starting point for building REST services<br />
https://spring.io/guides/tutorials/bookmarks/<br />

Good article describing ResponseEntityExceptionHandler<br />
http://www.springboottutorial.com/spring-boot-exception-handling-for-rest-services<br />

Other
Motivational quotes<br/>
http://javarevisited.blogspot.co.uk/2015/12/20-java-quotes-to-learn-and-motivate-yourself.html<br/>

Comprehensive list of backend interview questions<br />
https://github.com/arialdomartini/Back-End-Developer-Interview-Questions<br />

Clear description of port assignment in Kubernetes<br />
http://alesnosek.com/blog/2017/02/14/accessing-kubernetes-pods-from-outside-of-the-cluster/<br />

Good set of tricky interview questions
https://dzone.com/articles/top-20-java-interview-questions-with-answers<br/>


db.products.insert([
  { "description" : "T" } userId
  { "description" : "T2" }
  { "description" : "S1" }
])

db.sites.insert([
  { "url": "test", "originalPrice" : 100.00, "siteStatus": "ACTIVE", "productId" : "" }
  { "url": "test2", "originalPrice" : 100.00, "siteStatus": "ACTIVE", "productId" : "" }
  { "url": "s1", "originalPrice" : 100.00, "siteStatus": "ACTIVE", "productId" : "" }
  { "url": "blah", "originalPrice" : 100.00, "siteStatus": "INACTIVE", "productId" : "" }
])

db.scanResults.insert([
  { "scanPrice" : 99, scanStatus: "ELEMENT_FOUND", "httpStatus" : "FOUND", "scanDate" : ISODate("2019-03-26T00:00:00Z"), "siteId" : "" } userId
  { scanStatus: "ELEMENT_NOT_FOUND", "httpStatus" : "FOUND", "scanDate" : ISODate("2019-03-26T00:00:00Z"), "siteId" : "" }
  { "httpStatus" : "NOT_FOUND", "scanDate" : ISODate("2019-03-26T00:00:00Z"), "siteId" : "" }
])

db.sites.aggregate([
   {
      $lookup:
        {
            from: "scanResult",
            pipeline: [
              { $match:
                 { $expr:
                    { $and:
                       [
                         { $ne: [ "$httpStatus",  200 ] },
                         { $ne: [ "$scanStatus", "ELEMENT_FOUND" ] }
                       ]
                    }
                 }
              },
            localField: "id",
            foreignField: "siteId",
            as: "scanResults"
        }
   },
   { 
        $sort: { 
      	    scanDate: 1 
        } 
   },
   { 
   	    $limit : 1 
   },
   {
        $match: { 
            "scanResults": { 
                $ne: [] 
            } 
        }
   }
])

