
```java
// eventListener namespace
public class EventListener{
  public void onCarEnter(CarEnterEvent event){
    parkingController.enter(event);
  }
  public void onCarExit(CarExitEvent event){
    parkingController.exit(event);
  }
}


// controller namespace
public class ParkingController{  // singleton for controller
  private ParkingService parkingService;
	public Ticket enter(CarEnterEvent enterEvent){
        Car car = enterEvent.getCar();
        try{
            parkingService.enter(car);  // throw exception
            return printTicket(car)
        }
        catch(SpaceNotAvailableException e){
             displayMessage(e);
        }catch(Exception2 e){
            displayMessage(e);
        }
  }
  
  public Bill exit(CarExitEvent exitEvent){
    Car car = exitEvent.getCar();
    parkingService.exit(car);
    return printBill(car)
  }
  
  private Bill printBill(Car car){
  }
  
  private ticket printTicket(Car car){
  }
  
}


public class ReserveController{
  private ReserveService reverveService;
  public void reserve(Car car){
    try{
      reserveService.reserve(car);
    }catch(SpaceNotAvailabeException e){
    }
  }
}


//service namespace
public class ParkingService{
  public void enter(Car car) throws SpaceNotAvailableException, Exception2{       
        
  }
  
  public void exit(Car car) throws ticketDamageException{
          
  }
}


public class ReserveService{
  public void reserve(Car car) throws SpaceNotAvailableException{
  }
}



//model namespace
public class Car{
  private String plate;
  private CarType type;
}

public enum CarType{
  SmallCar("smallcar", "1"), Trunk("Trunk", "2");
  private String name;
  private String value;
  CarType(String name, String value){
    this.name = name;
    this.value = value;
  };
}




//dao namespace
// database Transaction




```
