### 自我介绍  
Hi, my name is Shusen Wu. You can call me Shusen. I am a graduate student from George Washington University majored in Computer Science with a 3.93 GPA and expected to graduate in May this year. I have about one year work experience and I am familiar with Python and JAVA. Besides, I have ever built a novel website with more than 1K users and sold it for about $1000. I built everything including database design, back-end design and UI design. Moreover, when I was an undergraduate, I led a team to built a campus application based on wechat without using any third-party code and had more than 5k users.  
___
### challenge project  
### Obstacle 
xueyiheng  
The most challenging project is an online course system. I did it during the internship. I was responsible for some back-end modules like course publishment and course review. It was challenging for me because I was an intern at that time and so many things were new for me. For example, I never used ActiveMQ and solr before. ActiveMQ is a middle-ware based on java message service and it sends message very fast. In this project, we used it to share messages between different systems. While solr is an open source search engine, like google, when people search a course, the solr will response to it. Because I was not familier with them at the beginning, I met many problems. For example, a problem I met is about message loss. When I sent some messages to the solr system using activeMQ, some of the messages would be lost. After viewing the error log and google this question, I found the solution. The reason of the problem is because after I sending the messages, I will close the connection after waiting for 15 seconds. Those messages I have sent will store on the buffer of the receiver’s system. The receiver can still read the messages from the buffer after the connection is closed. But if the receiver tries to send messages back, since the connection is already closed by me, the system will throw an socketException. And after that, the receiver cannot read the messages from buffer anymore. That is why some messages were lost. And the solution is simple, I chose to use transaction to commit the messages, instead of closing the connection after 15 seconds, the commit function will wait until the receiver closes the connection. I also met many other problems and bugs during this project which cost me a lot of time to solve them. Usually I would solve the bugs and finished the task on time even sacrifice some of my own time. I also learned that we need to focus on details, otherwise many bugs will appear.
___
### DDL
- 做没做过什么challenging的project，因为ddl而compromise一些东西什么的经历   
Couldn’t finish tasks before deadline  
I built a Chinese novel website and someone wanted to buy it. (Did you want to see the website, I can share you the link) Before buying it, the buyer want me to show her the whole website including management system and writer system. But at that time, the management system was not well built. Like for deleting a book, I can delete directly on the database so I didnot implement those functions on the management system. You know, she was the customer, I could not hold her for a long time to wait me to give her a demo. So I used one day to implement some fake functions on the management system and showed her the demo at the second day. And I also promised her that I will finished all those functions in a short days. The result was good, she was happy to buy the Chinese novel website and I also implemented those functions later with high quality. I also learned I can't sacrifice the customer experience or the quality of the product even there is a tight deadline.
 
- Tell me about a time when you worked against tight deadlines and didn’t have time to consider all options before making a decision.  
Sure, so, I have sold a novel website which was built by me. Then I was responsilbe for the webiste maintaince. One day, like about 3 months after selling the novel website, the buyer told me that all of the new chapters were wrong because there was no word in them which means those new chapters were empty. And the buyer asked me to fix the problem in a few hours cause it really hurt the users'  experience. This was a very tight deadline. So I had to fix it as fast as possible. I checked the system logs and found that the new chapters of novels collected by the web crawler could not be stored on the disk. But when I checked the avaialbe space on the disk, there still had more than 100 gigabytes. It confused me and I could not find the answer in such a short time. So, I decided to recover the system form the weekly backup image first to make sure the website run normally. There should be other options to solve this probelm, but I did not have much time to consider. 
After that, I found the reason of this bug. So, it was because the disk was run out of inodes. For a linux system, each file or folder will be assigned an inode to store the information about it. Once the system running out of inodes, it cannot create new files or folders on the disk even the space is enough. Since the novel websites had millions of chapters, it would need millions of inodes. From the experince, I learned the importance of the user experience and also learned many knowledges about linux system.
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
During the process, I often discussed with them about the logics. And I found one of the interns was quiet and seldom expressed his ideas. So I asked him privately that why he didnot discuss with us and share us his process. And he told me that he was stuck in the codes and didnot know how to do. He also mentioned that he was too shy to ask his mentor so many questions. You know, I had my own assignments with short deadlines which means I did not have much free time. But I also did not want him to get behind. Thus, I tried to help him through 3 ways. First, I read the requiremnts of his parts and share my ideas about how to do it with him. Secondly, I shared my codes with him so that he can learn and write his own codes. Thirdly, I helped him to debug when he could not solve by himself. He eventually catch up and liked to discuss with us. We also became friends during the process. My idea for this kind of situation is that we should not say that's not my job to take care of when we see teammates get behind. I know this is also the ownership principle of amazon.
___
### Conflict
disagree and commit
- Tell me a time you have a conflict with your teammate  
During my previous job, it was very common to have different ideas among teammates. Let me give you an example. One time I used the time  format to store date into database. While I saw other teammates conveted the datatime to a 13 digits format string and then stored into the database. Since datatime format is a very normal and easy way to store time, I told my teammates I disagree with using 13 digits format time rather than datatime format. My reason was that 13 digits format is difficult to read for human while datatime format is much more readable. Lately, the teamleader told me to use the 13 digits string format. I disagreed and commited. While I was modifing my codes, I found my idea was wrong. In this project, people did not read the time directly from the database, so 13 digits is readable or not was not our concern. Secondly, 13 digits string will save more space than datetime format since 13 digits only using 4 bytes while datetime using 8 bytes. Thirdly, 13 digits string format is more convenient for time comparing. From this experience, I leaned that Leaders are right a lot, I can argue my disagreements but I should disagree and commit. Besides, disgree and commit is not about justing saying it, I should try to prove myself was wrong. Once I realize I was wrong, it is more easy to accept other ideas.

___
### innovative
- Tell me a time you make something innovative  
It was about a project focused on student users called Jmubox which was designed and built by me. I was the team leader and I found some of my schoolmates to build it and run it together for about two years. In this project, I built an innovative function called emotional consultation. This function was to help students solve their emotional problems without going to campus mental health center. You know, many people like me are too shy to walk into the mental health enter. We cooperated with the campus mental health center so students can post their emotional questions on our system and teachers on campus mental health center will answer these questions. Though this way, we got 5 thousand student users. I am also very pround of this project not only because I was the team leader, but we also solved many students emotional problems.
___
### Fail
I have ever built a novel website and someone contacted me and wanted to buy it. But she want me change the user interface since she wanted the website focus on girls. For the first step, I spent about one week to use the photoshop to design the user interface including webpages, logos and some small decorations. But when I presented it with confidence, she was unhappy and told me that it needed significant work. At that time, I was also very disappointed, but I knew that I need to please the client by coming up with a new design. So I ask her for suggestions and what exactly she was looking for. She told me that those webpages were still boys' style while she wanted a girl's style website UI design. Besides, the dominant color was blue while she loved yellow. Moreover, She also wanted a very cute mascot as the logo of the website. Even though I am not a professional UI designer, I am a software engineer, I tried to modified the UI desigh based on her ideas. I adjusted the color scheme to yellow and made the style become more cute. I also found a very cute dynamic chook picture as the mascot and put it into the logo. During the process, I discussed many times with her about the design and modified again and again. And lady was completely satisfied with the website at the end. From the experience, I learned that I should have gotten a full understanding of what my client needed before jumping into the project.

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
Well, my long term goal for the two years graduate study was to get a high GPA. My GPA by now is 3.93. The reason why I insist on getting a high GPA is because my parents paid my tuition fee and I want use my GPA to prove I work hard to my parents. So for the two years study, I always sat in the front row of the classroom. My trick to get high GPA is to ask questions on every class frequently. Even though I do not have any questions, I will try to find one and ask. Because asking questions will help me focus more on the class.
Besides, it is far better to ask for clarification and solve an issue right away than to unsure. And I know that Amazon emphasizes teamwork. And constant communication with other teammates is very important. So I think my ability to ask questions would help me in the future work especially when I am new to the position.
___
### Risk
Speed is important.
- Tell me a time you take a risk but fail? What could you do better if you can do it again?   
-  Have you ever taken calculated risk and what if you failed with the risk  
___
### Ownership of the project
上面帮助队友
___
###  Learn new technology
你有没有自学过什么东西  
自发地学习什么工作Scope之外的东西。   
I started to learn Bootstrap from last week. Bootstrap is a very popular front-end framework. But I am a back-end guy not focus on front-end. The reason why I learned it is because I want to teach my girlfriend to built a personal blog website from front-end to back-end design. Our ideas about this blog website is that we use the github as our writer system. I mean, we wrote blogs on the github beacause it provides a very convient way to write blogs using markdown. And then we put the blog's link to our system. Our system will then read the html of the blog from github pages and show on our own website with our user interface. The way I learned Bootstrap was by reading the Bootstrap tutorial documents from W3school. It has many examples about Bootstraps' tags and classes. And I just read and tried to code these examples out one by one to see the results. I think the best way to learn it is using it. So, when after I reading most parts of the document on W3school, I will use it to built the blog website and that is also my original plan. Tought using it, I think I will not only practice it but also learn more new knowledges about it. Another concern is about getting into problems. I think there are many sources I can turn to for help. For example, I can ask my friends who focus on front-end for help. I can also check on the Internet by searching blogs or asking questions on Stack Overflow. 
___
Out of expectation  
###  超出supervisor预期的工作 
During my internship, there was an online course project. In this project, we often queried database tables and joined these tables together. You know, if we join many tables together, the SQL will become very long and complicated. I found every teammates did in this way. But I thought we could simplify the process. So I created a database view which join the tables. Throught this way, we did not need to write a long and complicated SQL each time to join tables but just queried the view insteadly. And eveyone was happy with it.
___
信息不够的事情
___
### what makes you most interested in a company.  
___
### array, arraylist, linklist, set 
- In java, array is a fixed size data structure while ArrayList is not. Array is more efficient than ArrayList.  
- Linkedlist is a linear data structure. The elements are not stored in contiguous locations. We linked elements by using pointers.  
- Hashset is based on hashmap. It put the element as the key into the hashmap. When the two keys are the same, the hashmap will update the value rather than create a new one.  
___
### 他们都问了有关array、linked list和hashmap的基本概念、操作和时间复杂度，尤其印度小哥问的非常详细，背后的实现机理都要解释  
- Array O(1) for appending an element to the end. O(n) for inserting because you need to shift the elements after the place where you insert.  
- Linked List: The time complexity for the Inserting at the end depends if you have the location of the last node, if you do, it would -be O(1) other wise you will have to search through the linked list and the time complexity would jump to O(n)  
- Hashmap O(1)  Structure: is an array consisting of linkedList. We will use a hashcode to search the element on the array. If two keys have the same corresponding hashcode, new value will be put into the tail of the linkedlist. 
___
### 图是什么，怎么存储，和树是什么区别     
- adjacency list, adjacency matrix, list of edges,  map to list
- Formally, a graph is an object consisting of a vertex set and an edge set. In machine leaning, I think people usually use adjacency matrix to present a graph while in normal algorithm questions, I think using adjacency list or a map to lists is a good way to present a graph. Of course, there are many other ways to present a graph, you can also design a class to present it.  
- Tree is also consisting of a set of vertexes. But in tree data structure, there is no loops. Besides, there is only one path between any two vertices. A tree can also be present as a graph. But a graph may not be present as a tree.
___
十分鐘口述LRU  
资源匮乏，怎么完成工作的    
有没有之前做过的东西，觉得可以做的更好些？  
  
What happens when you type in www.Amazon.com? DNS related  
What happens when your request is https /tls instead of http?  
___
### hashmap是不是都是O（1）查找，解释原因。 
No.   
[linkedList Node, linkedList Node A, ..., LinkedList]   Hashcode = hash(key) 链表部分如有N个同样的collision，就要O（n）
                       |
                   Linked Node B     
### 如何让字典有序
https://allenwind.github.io/2017/09/16/%E6%9C%89%E5%BA%8F%E5%AD%97%E5%85%B8%E7%9A%84%E5%AE%9E%E7%8E%B0/  
___
### 说两种sort 算法，解释对比  
___
- https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=516481&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26sortid%3D311  
- https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=514181&extra=page%3D2%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3089%5D%5Bvalue%5D%5B2%5D%3D2%26searchoption%5B3089%5D%5Btype%5D%3Dcheckbox%26searchoption%5B3046%5D%5Bvalue%5D%3D5%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26searchoption%5B3109%5D%5Bvalue%5D%3D1%26searchoption%5B3109%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline   
heap: insertion is often done by adding the new element at the end of the heap in the first available free space. This will generally violate the heap property, and so the elements are then sifted up until the heap property has been reestablished.   

### most interesting project
 


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

 
 
