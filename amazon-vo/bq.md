## DDL
- 做没做过什么challenging的project，因为ddl而compromise一些东西什么的经历   
Couldn’t finish tasks before deadline  
小黄鸡网站，收到邮件有人想买它，要我展示给buyer看。但是后台管理员模块那时候做得很不完善，因为之前是自己在用，比如删除书籍，我都是直接。于是在demo之前就花了1天时间添加了一些fake functions，包括书籍管理等。然后第二天展示给买家。因为买家不懂得技术，所以以为功能很完善，就愉快决定购买这个网站。但是我在之后花了一周时间把后台管理员功能都完善了。因为我不能sacrifice the customer experience or the quality of the product。我可以 sacrifice our own time to try to finish the tasks. 但是不能让产品质量不好。
It was about two years ago, I built a Chinese novel website and someone wanted to buy it. (Did you want to see the website, I can share you the link) Before buying it, the buyer want me to show her the whole website including management system and writer system. But at that time, the management system was not well built. Like for deleting a book, I can delete directly on the database so I didnot implement those functions on the management system. You know, she was the customer, I could not hold her for a long time to wait me to give her a demo. So I used one day to implement some fake functions on the management system and showed her the demo at the second day. And I also promised her that I will finished all those functions in a short days. The result was good, she was happy to buy the Chinese novel website and I also implemented those functions later with high quality. I also learned I can't sacrifice the customer experience or the quality of the product even there is a tight deadline.
 
- Tell me about a time when you worked against tight deadlines and didn’t have time to consider all options before making a decision.  
小黄鸡的网站，采集器无法存储新的章节，但是章节内容存进了数据库。导致用户看到的文章都是没有内容的，后来甚至导致进程一直抛出异常崩溃。因为急着修复，没有很多时间排查问题。只能先把日志文件下载下来然后恢复数据盘的镜像，让网站工作。  
Sure, so, I built a novel website and somone bought it. Then I was responsilbe for the webiste maintaince. One day, like about 3 months
after selling the novel website, the buyer told me that all of the new chapters were wrong because there was no word in them which means those new chapters were empty. And the buyer asked me to fix the problem in a few hours cause it really hurt the users'  experience. This was a very tight deadline. So I have to fix it as fast as possible. I checked the system logs and found that the new chapters of novels collected by the web crawler could not be stored on the disk. But I could not find the reasons. It was so weird because when I checked the size of the available space on the disk, I found there still had more than 100 gigabytes. It confused me and I did not have much time to do all the tests or check all system logs, service logs, envirment logs and all kinds of logs. So, I decided to recover the website system first. To make sure the website would run normally, I recovered the system from the weekly backup image. After that, I got time to check the logs carefully and also google the solution. So, it was because the disk was run out of inodes. For a linux system, each file or folder will be assigned an inode to store the information about it. Once the system running out of inodes, it cannot create new files or folders on the disk even the space is enough. Since the novel websites had millions of chapters, it would need millions of inodes. But when format a disk, by default, the system won't assigned so many inodes. From the experince, I learned the importance of the user experience and also learned many knowledges about linux system.
 
- Can’t catch up DDL? What did you do?  
___
- Tell me a time your teammate struggled, how do you help him/her?  
It was during my internship, I was assigned to do some modules for an online course system along with another two student interns. 
During the process, I often discussed with them about the logics. And I found one of the interns was quiet and seldom expressed his ideas. So I asked him privately that why he didnot discuss with us and share us his process. And he told me that he was stuck in the codes and didnot know how to do. He also mentioned that he was too shy to ask his mentor so many questions. You know, I had my own assignments with short deadlines which means I did not have much free time. But I also did not want him to get behind. Thus, I tried to help him through 3 ways. First, I read the requiremnts of his part and share my idea how to do it. Second, I shared my codes with him so that he can learn and write his own codes. Third and finally, I helped him to debug when he could not solve by himself. He eventually catch up and liked to discuss with us. We also became friends during the process.  
___

Tell me a time you made a decision without your manager or mentor.  
one time without manager decision and fail  
One time that your method was wrong  

- What is your most interesting bug?
- Tell me a time you make something innovative
- Tell me a time you take a risk but fail? What could you do better if you can do it again? 
- Tell me a time you have a conflict with your teammate


- What is the most challenging project you have done? What did you learn from it？ Why would you prefer using this tech stack over different tech stack?
- Exp of feedback to others/others to you.
- Can’t catch up DDL? What did you do?
- Why Amazon?
问你一个坚持的长期的goal是什么，以及你为什么要坚持。  


自我介绍  
the most challenge project, how will you find resources when you cannot access to your metor?
one time without manager decision and fail  
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

### most interesting project
### conflict with team members
### Tell me about a time when you were wrong.

### most pround project
#### Jmubox    
- It is a campus service application based on wechat and I never used any third-party code for wechat to build our system. I was the team leader and I found some of my schoolmates to build it and run it together for about two years. My job was to do all the back-end part including some front-end interactions. Besides, the logos and posters were also designed by me by using photoshop. It provided students many functions like matching another student to chat through our system. Or you can query your personal transcript by binding your school account to our system. And our unique purpose for this project was to help students solve some emotional questions without going to campus mental health center. Students can post their emotional questions to jumbox and our teammates as well as a teacher in campus mental health center will be responsible for answering these questions. I am pround of it not only because I was the team leader, but we also solved many students emotional problems. 从中学到了什么

### most challenge project
#### xueyiheng   
The most challenging project is an online course system. I did it during the internship. I was responsible for some back-end modules like course publishment and course review. It was challenging for me because I was an intern at that time and so many things were new for me. For example, I never used ActiveMQ and solr before. ActiveMQ is a middle-ware based on java message service and it sends message very fast. In this project, we used it to share messages between different systems. While solr is an open source search engine, like google, when people search a course, the solr will response to it. Because I was not familier with them at the beginning, I met many problems. For example, a problem I met is about message loss. When I send some messages to the solr system using activeMQ, some of the messages will lost. After viewing the error log and google this question, I found the solution. The reason of the problem is because after I sending the messages, I will close the connection after waiting for 15 seconds. Those messages I have sent will store on the buffer of the receiver’s system. The receiver can still read the messages from the buffer after the connection is closed. But if the receiver tries to send messages back, since the connection is already closed by me, the system will throw an socketException. And after that, the receiver cannot read the messages from buffer anymore. That is why some messages are lost. And the solution is simple, I choose to use transaction to commit the messages, instead of closing the connection after 15 seconds, the commit function will wait until the receiver closes the connection. I also met many other problems and bugs during this project which cost me a lot of time to solve them. Usually I would solve the bugs and finished the task on time even sacrifice some of my own time. Because I did not want to 
leave my teammates an impression that an intern can't do job fast and good. At the end, I earned their trust cause I always finished the tasks well.从中学到了什么？关注细节，才能提高产品质量。

- What I did  
I did the online course system during the internship. I was responsible for some back-end modules like course publishment and course review. I am gonna share you an example of what I did. When someone publishes a course successfully, I wrote the code to query the database and provided functions for the module of course review, like some functions to allow the course to be published or refused to be pulished. This part was simple, just some query functions. And after the course is reviewed and allowed to be published, my job is to synchronize the data to the Solr service. Solr is an opensource search engine, like google, when people search a course, the solr will response to it. I used ActiveMQ to synchronize the data to the solr system. ActiveMQ is a middle-ware based on java message service and it sends message very fast. I used the producer and consumer pattern. So, when a course is published, it is like a producer and produce the course information as a message, and the search engine solr will receive the message like a consumer. Once the data is synchronized to the solr engine, people can search and find the course on our system.

- Difficulty  
A problem I met is about message loss. When I send some messages to the solr system using activeMQ, some of the messages will lost. After viewing the error log and google this question, I found the answer. So, after I sending the messages, I will close the connection after waiting for 15 seconds. Those messages I have sent will store on the buffer of the receiver’s system. The receiver can still read the messages from the buffer after the connection is closed. But if the receiver tries to send messages back, since the connection is already closed by me, the system will throw an socketException. And after that, the receiver cannot read the messages from buffer anymore. That is why some messages are lost. And the solution is simple, I choose to use transaction to commit the messages, and the commit function will wait until the receiver closes the connection.

 

### Why Amazon
### step out and help someone
