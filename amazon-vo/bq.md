就是如果项目时间特别紧，你会怎么做啊，要不要也帮帮你没完成的小老弟？还有就是如果要做决定的话你会考虑什么问题啊？我都是先说了自己怎么做，小哥问我有没有具体的实例  
array arraylist linklist 区别.  
图是什么，怎么存储，和树是什么区别  
他们都问了有关array、linked list和hashmap的基本概念、操作和时间复杂度，尤其印度小哥问的非常详细，背后的实现机理都要解释，
还有树的三种遍历的定义、BFS和DFS等。  
第一个BQ有点常规，问目前在做啥project。第二个BQ有点不常规，问你一个坚持的长期的goal是什么，以及你为什么要坚持   
BQ問最近學了什麼technical skill，怎麼學的  
BQ tight deadline 
十分鐘口述LRU
what makes you most interested in a company.    
hashmap是不是都是O（1）查找，解释原因。 然后说两种sort 算法，解释对比  
- https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=516481&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26sortid%3D311  
- https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=514181&extra=page%3D2%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3089%5D%5Bvalue%5D%5B2%5D%3D2%26searchoption%5B3089%5D%5Btype%5D%3Dcheckbox%26searchoption%5B3046%5D%5Bvalue%5D%3D5%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D1%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline


### most pround project
#### Jmubox    
- It is a campus service application based on wechat and I never used any third-party code for wechat to build our system. I was the team leader and I found some of my schoolmates to build it and run it together for about two years. My job was to do all the back-end part including some front-end interactions. Besides, the logos and posters were also designed by me by using photoshop. It provided students many functions like matching another student to chat through our system. Or you can query your personal transcript by binding your school account to our system. And our unique purpose for this project was to help students solve some emotional questions without going to campus mental health center. Students can post their emotional questions to jumbox and our teammates as well as a teacher in campus mental health center will be responsible for answering these questions. I am pround of it not only because I was the team leader, but we also solved many students emotional problems. 

### most challenge project
#### xueyiheng   
The most challenging project is an online course system. I did it during the internship. I was responsible for some back-end modules like course publishment and course review. It was challenging for me because I was an intern at that time and so many things were new for me. For example, I never used ActiveMQ and solr before. ActiveMQ is a middle-ware based on java message service and it sends message very fast. In this project, we used it to share messages between different systems. While solr is an open source search engine, like google, when people search a course, the solr will response to it. Because I was not familier with them at the beginning, I met many problems. For example, a problem I met is about message loss. When I send some messages to the solr system using activeMQ, some of the messages will lost. After viewing the error log and google this question, I found the solution. The reason of the problem is because after I sending the messages, I will close the connection after waiting for 15 seconds. Those messages I have sent will store on the buffer of the receiver’s system. The receiver can still read the messages from the buffer after the connection is closed. But if the receiver tries to send messages back, since the connection is already closed by me, the system will throw an socketException. And after that, the receiver cannot read the messages from buffer anymore. That is why some messages are lost. And the solution is simple, I choose to use transaction to commit the messages, instead of closing the connection after 15 seconds, the commit function will wait until the receiver closes the connection. I also met many other problems and bugs during this project which cost me a lot of time to solve them. Usually I would solve the bugs and finished the task on time even sacrifice some of my own time. Because I did not want to 
leave my teammates an impression that an intern can't do job fast and good. At the end, I earned their trust cause I always finished the tasks well.

- What I did  
I did the online course system during the internship. I was responsible for some back-end modules like course publishment and course review. I am gonna share you an example of what I did. When someone publishes a course successfully, I wrote the code to query the database and provided functions for the module of course review, like some functions to allow the course to be published or refused to be pulished. This part was simple, just some query functions. And after the course is reviewed and allowed to be published, my job is to synchronize the data to the Solr service. Solr is an opensource search engine, like google, when people search a course, the solr will response to it. I used ActiveMQ to synchronize the data to the solr system. ActiveMQ is a middle-ware based on java message service and it sends message very fast. I used the producer and consumer pattern. So, when a course is published, it is like a producer and produce the course information as a message, and the search engine solr will receive the message like a consumer. Once the data is synchronized to the solr engine, people can search and find the course on our system.

- Difficulty  
A problem I met is about message loss. When I send some messages to the solr system using activeMQ, some of the messages will lost. After viewing the error log and google this question, I found the answer. So, after I sending the messages, I will close the connection after waiting for 15 seconds. Those messages I have sent will store on the buffer of the receiver’s system. The receiver can still read the messages from the buffer after the connection is closed. But if the receiver tries to send messages back, since the connection is already closed by me, the system will throw an socketException. And after that, the receiver cannot read the messages from buffer anymore. That is why some messages are lost. And the solution is simple, I choose to use transaction to commit the messages, and the commit function will wait until the receiver closes the connection.

### Couldn’t finish tasks before deadline

### Why Amazon
### step out and help someone
