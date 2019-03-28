```java
//controller namespace
public class ReserveController{
    private ReserveService reserveService;
    
    public Ticket reserve(String startTime, String endTime, String UserId, String TypeId){
      try{
      
      }catch(TimeConflictException e){
        replyMessage(e);
      }
    }

}

//service namespace
public class ReserveService{
    public void reserve(Order order) throws TimeConflictException{
      //first, check timeConflict
      if(check(Order)){
          throw new TimeConflictException("xxxx");
      }else{
         addOrder(Order); 
      }
    }
}

//model namespace
public class Order{
  private String startTime;
  private String endTime;
  private OrderType order;
  private String UserId;
}

public enum OrderType{
    BigRoom('bigroom', '1'), SmallRoom('smallroom', '2');
    private String name;
    private String value;
}

```
