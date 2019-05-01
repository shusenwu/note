### 自我介绍  
Hi, my name is Shusen Wu. You can call me Shusen. I am a graduate student from George Washington University majored in Computer Science with a 3.93 GPA and expected to graduate in May this year. I have about one year work experience and I am familiar with Python and JAVA. Besides, I have ever built a novel website with more than 1K users and sold it for about $1000. I built everything including database design, back-end design and UI design. Moreover, when I was an undergraduate, I led a team to built a campus application based on wechat without using any third-party code and had more than 5k users.  
___
### challenge project  
### Obstacle 
xueyiheng  
The most challenging project is an online course system. I did it during the internship. I was responsible for some back-end modules like course publishment and course review. It was challenging for me because I was an intern at that time and so many things were new for me. For example, I never used ActiveMQ and solr before. ActiveMQ is a middle-ware based on java message service and it sends message very fast. In this project, we used it to share messages between different systems. While solr is an open source search engine, like google, when people search a course, the solr will response to it. Because I was not familier with them at the beginning, I met many problems. For example, a problem I met is about message loss. When I send some messages to the solr system using activeMQ, some of the messages will lost. After viewing the error log and google this question, I found the solution. The reason of the problem is because after I sending the messages, I will close the connection after waiting for 15 seconds. Those messages I have sent will store on the buffer of the receiver’s system. The receiver can still read the messages from the buffer after the connection is closed. But if the receiver tries to send messages back, since the connection is already closed by me, the system will throw an socketException. And after that, the receiver cannot read the messages from buffer anymore. That is why some messages are lost. And the solution is simple, I choose to use transaction to commit the messages, instead of closing the connection after 15 seconds, the commit function will wait until the receiver closes the connection. I also met many other problems and bugs during this project which cost me a lot of time to solve them. Usually I would solve the bugs and finished the task on time even sacrifice some of my own time. Because I did not want to leave my teammates an impression that an intern can't do job fast and good. At the end, I earned their trust cause I always finished the tasks well. I also learned that we need to focus on details, otherwise many bugs will appear.
___
### DDL
- 做没做过什么challenging的project，因为ddl而compromise一些东西什么的经历   
Couldn’t finish tasks before deadline  
I built a Chinese novel website and someone wanted to buy it. (Did you want to see the website, I can share you the link) Before buying it, the buyer want me to show her the whole website including management system and writer system. But at that time, the management system was not well built. Like for deleting a book, I can delete directly on the database so I didnot implement those functions on the management system. You know, she was the customer, I could not hold her for a long time to wait me to give her a demo. So I used one day to implement some fake functions on the management system and showed her the demo at the second day. And I also promised her that I will finished all those functions in a short days. The result was good, she was happy to buy the Chinese novel website and I also implemented those functions later with high quality. I also learned I can't sacrifice the customer experience or the quality of the product even there is a tight deadline.
 
- Tell me about a time when you worked against tight deadlines and didn’t have time to consider all options before making a decision.  
Sure, so, I have sold a novel website which was built by me. Then I was responsilbe for the webiste maintaince. One day, like about 3 months after selling the novel website, the buyer told me that all of the new chapters were wrong because there was no word in them which means those new chapters were empty. And the buyer asked me to fix the problem in a few hours cause it really hurt the users'  experience. This was a very tight deadline. So I have to fix it as fast as possible. I checked the system logs and found that the new chapters of novels collected by the web crawler could not be stored on the disk. But I could not find the reasons. It was so weird because when I checked the size of the available space on the disk, I found there still had more than 100 gigabytes. It confused me and I did not have much time to do all the tests or check all system logs, service logs, envirment logs and all kinds of logs. So, I decided to recover the website system first. To make sure the website would run normally, I recovered the system from the weekly backup image. After that, I got time to check the logs carefully and also google the solution. So, it was because the disk was run out of inodes. For a linux system, each file or folder will be assigned an inode to store the information about it. Once the system running out of inodes, it cannot create new files or folders on the disk even the space is enough. Since the novel websites had millions of chapters, it would need millions of inodes. But when format a disk, by default, the system won't assigned so many inodes. From the experince, I learned the importance of the user experience and also learned many knowledges about linux system.
- Can’t catch up DDL? What did you do?  
Basically, if there is a manager or a mentor, I will tell him the situation and ask him for advices cause I do not have much work experience as a new grad. But I will prevent not to sacrifice customers' or users' experience and still make my codes with high quality. Would you want me to share you with some detail experience? It was about a Chinese novel website, I built that website and someone wanted to buy it.

- miss deadline  
I was once assigned an one-person project to build a system to seperate cold-hot tables based on database. I believed I could finished it in five days in addition to the workdload I already had. So I told the manager that I could finished it in 5 weekdays, but actually I miscalculated how long it would take me to write it. When the last day the project was due, I realized I would not finished it in time. 
So I apologized to the manager and explained what happened. I also asked two more days to finished it and the manager granted. From this experience, I learned that I need to be honest with myself about the workload I can handle each day. I also learned that I need to include a time buffer to ensure I can meet the deadlines in time even if some unforeseen events happen. Besides, if I could not estimate the time from the start, I should discuss with my mentor or manager first and then share my timeline with them to make sure the project is going well as expected. 

- Tight Schedule

___
### teammates
- Tell me a time your teammate struggled, how do you help him/her?  
It was during my internship, I was assigned to do some modules for an online course system along with another two student interns. 
During the process, I often discussed with them about the logics. And I found one of the interns was quiet and seldom expressed his ideas. So I asked him privately that why he didnot discuss with us and share us his process. And he told me that he was stuck in the codes and didnot know how to do. He also mentioned that he was too shy to ask his mentor so many questions. You know, I had my own assignments with short deadlines which means I did not have much free time. But I also did not want him to get behind. Thus, I tried to help him through 3 ways. First, I read the requiremnts of his part and share my idea how to do it. Second, I shared my codes with him so that he can learn and write his own codes. Third and finally, I helped him to debug when he could not solve by himself. He eventually catch up and liked to discuss with us. We also became friends during the process.  
- Tell me a time you have a conflict with your teammate  
Sure, let me tell you a time when I had a conflict with my teammate during my internship, I was assigned to do some modules for an online course system along with another two student interns. Let's called these two interns A and B respectively. So A was responsible for builting some APIs which would be used by B. However, it seems the APIs written by A had some bugs which caused B's codes throw errors frequently and it also affected B's process that B could not finished his task fast. So B often blamed A in public loudly and let everybody knowed that A's APIs had many bugs. I thought B's behavior was wrong. So I told B privately that do not always blame A in public which will make A awkward. I also asked B to help A debug together. But B refused me and disagree with me. He kept blaming A loudly. So it also became a conflict between B and me. To solve this situation, I tried to comfort A and help him to debug. Besides, I also told HR the situation that B always blamed A in public. At the end, B left the company and A finished all his work well.
___
### innovative
- Tell me a time you make something innovative  
It was about a project focused on student users called Jmubox which was designed and built by me. I was the team leader and I found some of my schoolmates to build it and run it together for about two years. In this project, I built an innovative function called emotional consultation. This function was to help students solve their emotional problems without going to campus mental health center. You know, many people like me are too shy to walk into the mental health enter. We cooperated with the campus mental health center so students can post their emotional questions on our system and teachers on campus mental health center will answer these questions. Though this way, we got 5 thousand student users. I am also very pround of this project not only because I was the team leader, but we also solved many students emotional problems.
___
### Fail
It was about two years ago before my graduate study. A lady contacted me and asked me to design and build a Chinese novel website for her. For the first step, I spent about one week to use the photoshop to design the user interface including webpages, logos and some small decorations. But when I presented it with confidence, she was unhappy and told me that it needed significant work. At that time, I was also very disappointed, but I knew that I need to please the client by coming up with a new design. So I ask her for suggestions and what exactly she was looking for. She told me that those webpages were boys' style while she wanted the website focused on girls' novel. So she wanted a girl's style website UI design. Besides, the dominant color was blue while she loved yellow. Moreover, She also wanted a very cute mascot as the logo of the website. Even though I am not a professional UI designer, I am a software engineer, I tried to modified the UI desigh based on her ideas. I adjusted the color scheme to yellow and made the style become more cute. I also found a very cute dynamic chook picture as the mascot and put it into the logo. During the process, I discussed many times with her about the design and modified again and again. And lady was completely satisfied with the website at the end. From the experience, I learned that I should have gotten a full understanding of what my client needed before jumping into the project.

___
### Mistake
### One time that your method was wrong  
没有及时沟通，修改问题。  
During my first internship, when I met some questions, I was too shy to ask for clarification. At first, I thought keep silence was a good way to solve questions independent. For example, in the online course project, I need to store course publishment time to the database. But in the requirement document, it did not metioned which time format I should use. So, I hesitated for a second then I chose the normal datatime format. However, in this project, all other teammates conveted the timedate to a 13 digits format string and then stored into the database. Cause my datetime format was not compatible with the others, I had to modify my codes. Since then, I always ask for clarification if necessary. From this experience, I have learned that it is far better to ask for clarification and solve an issue right away than to unsure. And I know that Amazon emphasizes teamwork and constant communication with other teammates is very important. So I think my ability to ask questions of my peers would help me in the future work especially when I am new to the position.

___
### Bug
小黄鸡的inodes 和 xueyiheng的Message lost
- What is your most interesting bug?

___
### Weakness
Exp of feedback to others/others to you.
对自己的代码太自信，然后不仔细检查就说自己做完了。
___
### Decision
One time without manager decision and fail  
有个人想要找我开发一个小说站，但是我不是专业的UI design,也找不到人来负责做这个设计。因为我会PS，所以我就决定自己来做。结果对方不满意这个设计。
   
one time change your decision later?    
Tell me a time you take a risk but fail? What could you do better if you can do it again?   
还有就是如果要做决定的话你会考虑什么问题啊？  
快速决定  
小黄鸡系统崩溃，是要马上恢复系统，还是先test and find the answer再恢复。
___
- how will you find resources when you cannot access to your metor?  
It depends on what resources I need. If I need some tools or materials for the project, let's say I need a server to run the codes. I guess I can always find someone in the company and ask for the resource. If I need some help, let's say I need someone to help me debug my codes, I will google and do it by myself first. If I still can't solve it, I can ask my peers and other teammates for help. And I think making friends with teammates is important since it is easier to ask a friend for help.
___
- Why Amazon?
___
问你一个坚持的长期的goal是什么，以及你为什么要坚持。  

___
### Risk
-  Have you ever taken calculated risk and what if you failed with the risk  
___
Out of expectation  
自我介绍 有意思的项目 为什么用这个算法 你的数据量多大 跑了多久 你有没有遇到什么问题 你是怎么发现解决的 你改进之后提升了多少  你队友和你意见不一样的地方 你是怎么说服他们的 你有没有队友偷懒你只能自己做的经历  
信息不够的事情
array arraylist linklist 区别.  
图是什么，怎么存储，和树是什么区别    
自发地学习什么工作Scope之外的东西。  
adjacency list, adjacency matrix, list of edges,  
他们都问了有关array、linked list和hashmap的基本概念、操作和时间复杂度，尤其印度小哥问的非常详细，背后的实现机理都要解释，
还有树的三种遍历的定义、BFS和DFS等。  
第一个BQ有点常规，问目前在做啥project。第二个BQ有点不常规，问你一个坚持的长期的goal是什么，以及你为什么要坚持   
BQ問最近學了什麼technical skill，怎麼學的   
 先问了树和图，什么时候一个图是一棵树，让我写下来，我说没有环的图就是树。接下来，问题： 如何判断一个有向图是不是有环  
十分鐘口述LRU
what makes you most interested in a company.    
What happens when you type in www.Amazon.com? DNS related  
What happens when your request is https /tls instead of http?  
  
hashmap是不是都是O（1）查找，解释原因。 然后说两种sort 算法，解释对比  
- https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=516481&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26sortid%3D311  
- https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=514181&extra=page%3D2%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3089%5D%5Bvalue%5D%5B2%5D%3D2%26searchoption%5B3089%5D%5Btype%5D%3Dcheckbox%26searchoption%5B3046%5D%5Bvalue%5D%3D5%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D1%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline   
heap: insertion is often done by adding the new element at the end of the heap in the first available free space. This will generally violate the heap property, and so the elements are then sifted up until the heap property has been reestablished.   

### most interesting project
 
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

 
 
