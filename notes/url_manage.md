- [x] logic of seedurl and changes

the management of seedURl;  
Q1:how does the project achieve seedurl?  
A1:creat a class named seedurl to manage the seedurl.  
Q2:How is the new url passed into ispider？  
A2:by ```url = jedis.lpop(key);``` in MyredisSource.    
Q3:what is the useage of repository?  
A3:management of seedurl
      
seedurl:[hippopx](https://www.hippopx.com/)



steps:
- [x] find all places about seedurl
| location     | changes |
| ----------- | ----------- |
| ISpider.seedUrls  | JD $\rightarrow$ hippopx       |



- [x] url management based on Streaming computing framework
Actuall, this part I assume I already get the url by spider. what I need to understand is three part:
1. how to start the flink and set flink evrionment
   ``` StreamExecutionEnvironment env =
       StreamExecutionEnvironment.getExecutionEnvironment();
        env.setParallelism(4); 
3. figure out the level of url:the way of judgement.
   firstly,get the whole html by httputil.
5. sinkfunction: how to store the url
6. how to get the new url from flink.  
 
---
 now I need change the url management and distrubution for our target website.
      anylize the website structure:which one is higher or lower?  
      set the level judgementexe  
      set the new condition for url management:

what I need for url_anylisis part:
1.get all urls
2.get the picture data
