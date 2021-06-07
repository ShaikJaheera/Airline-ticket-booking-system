# Airline-ticket-booking-system
Requirements:
1st user should ask about login or register options
1.login
2.register
3.exit
if user choose register option then the following credentials should be filled
enter name:
enter mobile number:
enter government id:
enter date of birth:
enter emailid:
enter password:
all the credentials should be filled.
if the user is already registed the details, then the user can directly login insted of registration.
login details are as follows:
enter mobile number:
enter password:
then the user gets 3 options
1.book fligt
2.history
3.exit
based on users choice user can choose the options.
if the user chooses option 1. user can book the available tickets, if no flight is available then user can choose other flight options
if user uses option 2 user can check the history of flights being booked by him/her.
3. to exit 
the user has again options he may login or register or exit based on his choice


//verifying the new register for existing
	public static boolean verityInfoOfNewRegister(List<UserDetails> user,String phNum)
	{
		for(UserDetails d:user) 
		{
			if(d.getMobNum().equals(phNum)) return false;
		}
		return true;
	}	
 if the user id has registerd then it shows user id has be already existed!...
 
        
      // registration details.....................
        
	public static Travels bookTicket(AllFlights flight) 
	{
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String name, age, flightName, from, to, startTime, endTime, price;
		try 
		{
			System.out.println("enter name:");
			name = br.readLine();
			System.out.println("enter age:");
			age = br.readLine();
			flightName = flight.getFlightName();
			from = flight.getFrom();
			to = flight.getTo();
			startTime = flight.getStartTime();
			endTime = flight.getEndTime();
			price = flight.getPrice();
			Travels journey = new Travels(name, age, flightName, from, to, startTime, endTime, price);
			System.out.println("booking your ticket...");
			try 
			{
				Thread.sleep(1000);
				System.out.println("ticket booked successfully...!\n");
			} 
			catch (InterruptedException e) 
			{
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			return journey;
			
			
		} 
		catch (IOException e) 
		{
			// TODO Auto-generated catch block
			e.printStackTrace();
			System.out.println("error occured, try again...");
			return null;
		}
	}
 the above are details for the user to register... the block of code is kept in try and catch blocks to handle exceptions occured during registration processs.......
        
        
        // login the user
	
	private static int loginUser(List<UserDetails> userInfo,String mobNum, String password) 
	{
		
		for(int i=0;i<userInfo.size();i++) 
		{
			if(userInfo.get(i).getMobNum().equals(mobNum) && userInfo.get(i).getPassword().equals(password)) return i;
		}
		System.out.println("Not valid user\nTry register....");
		return -1;
	}
                                                   
                                                   
  if the user is already registered he/she can directly login by giving mobile number and password used while registering. 
 
          
   // main method logic...
	
	
	public static void main(String[] args) 
	{
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		List<UserDetails> userInfo = new ArrayList<>();
		
		List<AllFlights> allFlights = new ArrayList<>();  
		
		allFlights.add(new AllFlights("Indigo","hyderabad","vijayawada","1:00pm","4:30pm","3499"));
		allFlights.add(new AllFlights("Redbus","hyderabad","mumbai","13:00","24:00","9900"));
		allFlights.add(new AllFlights("KingFisher","chennai","mumbai","8:40","3:20","2000"));
		allFlights.add(new AllFlights("Versa","bangalore","hyderabad","19:45","23:50","35500"));
		allFlights.add(new AllFlights("Truejet","andaman","srilanka","22:25","12:50","100000"));
		allFlights.add(new AllFlights("GoInia","Chennai","hyderabad","4:00","10:30","3800"));
		allFlights.add(new AllFlights("kingfisher","hyderabad","goa","15:20","23:40","10000"));
        
        
    its is the array, and list of all the availabile flights along with timings, price, from, and destination................................
		
		int choice  = 0;
		do 
		{
			System.out.println("\n1.Register\n2.Login\n3.Exit");
			try 
			{
				choice = Integer.parseInt(br.readLine());
			} 
			catch (NumberFormatException | IOException e) 
			{
				System.out.println("Invalid entry\nenter valid choice..");
				continue;
			}
        
       this is to show the available options to the user
        1. register
        2. login
        3. history, options should be take in number format, or else it throws errors............
        
			switch(choice) 
			{
				case 1: 
				{
					UserDetails adding = userRegistration(userInfo);
					if(adding != null) 
					{
						userInfo.add(adding);
					}
				}
				break;
        
       this is for adding users details during registration

				case 2: 
				{
					String mobNum,password;
					try 
					{
						System.out.println("Enter MobileNumber:");
						mobNum = br.readLine();
						System.out.println("Enter Password:");
						password = br.readLine();
						int index = loginUser(userInfo,mobNum,password);
        // user details are taken
						if(index != -1) 
						{
							int userChoice = 0;
							do 
							{
								System.out.println("\n1.BookTicket\n2.History\n3.Exit");
								try 
								{
									userChoice = Integer.parseInt(br.readLine());
									switch(userChoice) 
									{
									case 1: 
									{
										int i=1;
										String from,to;
										System.out.println("From...");
										from = br.readLine().toLowerCase();
										System.out.println("To");
										to = br.readLine().toLowerCase();
										boolean noFlight = true;
										List<AllFlights> availbleFlights = new ArrayList<>();
										for(AllFlights list:allFlights)
										{
											if(list.getFrom().equals(from) && list.getTo().equals(to)) 
											{
												System.out.println(i++ +"-->"+ list);
												availbleFlights.add(list);
												noFlight = false;
											}
										}
										if(noFlight) 
										{
											System.out.println("no flights found in the route?");
											continue;
										}
									
										int flightChoice= Integer.parseInt(br.readLine());
										if(flightChoice>0 && flightChoice<=availbleFlights.size())
										{
											Travels userJourney = bookTicket(availbleFlights.get(flightChoice-1));
											userInfo.get(index).setFlightBookings(userJourney);
										}
										else 
										{
											System.out.println("entry wrong...");
											continue;
										}
									
									}
									break;
                                                                        
                                                                        
                    // after user is logged in then if the user chooses the option as BOOK TICKET then it asks to and from adress if the fligts are available it shows the list
                    or else it shows flights not available........................
                    
                    
                    
                    
									case 2: 
									{
										if(userInfo.get(index).getFlightBookings().size()==0) 
										{
											System.out.println("no recent booking....!");
											continue;
										}
										for(int i=0;i<userInfo.get(index).getFlightBookings().size();i++) 
										{
											System.out.println(userInfo.get(index).getFlightBookings().get(i));
										}
									}
									break;
                // its is to ckeck the history of tickets being booked by the user .... if no tickets are booked till now it shows no history..................
        
        
        
								case 3:	System.out.println("Logging you out..."); 
										break;
        
		// if the user want to log out, user can choose option 3.. 
        
								default: System.out.println("invalid entry made...");
										break;
       // if no entry matches ie 1 2 3 excepts this numbers if the user chooses other numbers it shows invalid entry.......................
							}
						}
						catch(IOException e) 
						{
							System.out.println("Invalid entry"); 
							continue;
						}
						}while(userChoice != 3);
					}
					
				} 
				catch(IOException e)
				{
					
				}
			}
			break;
			case 3: System.out.println("Exiting...");
				break;
			default: System.out.println("Invalid choice");
			}
	// to exit from the log in option..............................
		}while(choice != 3);
		
		
	}
 }
        
        
   // to check availability of flight name, from, to, starttime, endtime, price of the flight     
        class AllFlights 
        {
	private String flightName,from,to,startTime,endTime,price;
	
	public AllFlights(String flightName, String from, String to, String startTime, String endTime, String price)
	{
		super();
		this.flightName = flightName;
		this.from = from;
		this.to = to;
		this.startTime = startTime;
		this.endTime = endTime;
		this.price = price;
	}


	public String toString()
	{
		return "ListOfFlights [flightName=" + flightName + ", from=" + from + ", to=" + to + ", startTime=" + startTime
					+ ", endTime=" + endTime + ", price=" + price + "]";
	}

	public String getFlightName() 
	{
		return flightName;
	}

	public void setFlightName(String flightName) 
	{
		this.flightName = flightName;
	}

	public String getFrom() 
	{
		return from;
	}

	public void setFrom(String from)
	{
		this.from = from;
	}

	public String getTo()
 	{
		return to;
	}

	public void setTo(String to) 
	{
		this.to = to;
	}

	public String getStartTime() 
	{
		return startTime;
	}

	public void setStartTime(String startTime) 
	{
		this.startTime = startTime;
	}

	public String getEndTime() 
	{
		return endTime;
	}

	public void setEndTime(String endTime) 
	{
		this.endTime = endTime;
	}

	public String getPrice() 
	{
		return price;
	}

	public void setPrice(String price) 
	{
		this.price = price;
	}
}

   
        
 // to check the user flight tickets booking history.......................!       
   
 class Travels 
{
	private String name,age,flightName,from,to,startTime,endTime,price;
	
	public Travels(String name, String age, String flightName, String from, String to, String startTime, String endTime, String price)
	{
		super();
		this.name = name;
		this.age = age;
		this.flightName = flightName;
		this.from = from;
		this.to = to;
		this.startTime = startTime;
		this.endTime = endTime;
		this.price = price;
	}

	@Override
	public String toString()
	{
		return "Journey [name=" + name + ", age=" + age + ", flightName=" + flightName + ", from=" + from + ", to=" + to
				+ ", startTime=" + startTime + ", endTime=" + endTime + ", price=" + price + "]";
	}

	public String getName()
 	{
		return name;
	}

	public void setName(String name) 
	{
		this.name = name;
	}

	public String getAge() 
	{
		return age;
	}

	public void setAge(String age) 
	{
		this.age = age;
	}

	public String getFlightName() 
	{
		return flightName;
	}

	public void setFlightName(String flightName) 
	{
		this.flightName = flightName;
	}

	public String getFrom() 
	{
		return from;
	}

	public void setFrom(String from) 
	{
		this.from = from;
	}

	public String getTo() 
	{
		return to;
	}

	public void setTo(String to) 
	{
		this.to = to;
	}

	public String getStartTime() 
	{
		return startTime;
	}

	public void setStartTime(String startTime) 
	{
		this.startTime = startTime;
	}

	public String getEndTime() 
	{
		return endTime;
	}

	public void setEndTime(String endTime) 
	{
		this.endTime = endTime;
	}

	public String getPrice() 
	{
		return price;
	}

	public void setPrice(String price) 
	{
		this.price = price;
	}

}
        
   // to take the user details..........................!     
        
    class UserDetails 
{
	private String name,mobileNumber,govId,dob,emailId,password;
	private List<Travels> travels = new ArrayList<>();
	public UserDetails(String name, String mobNum, String govId, String dob, String email, String password) 
	{
		super();
		this.name = name;
		this.mobileNumber = mobNum;
		this.govId = govId;
		this.dob = dob;
		this.emailId = email;
		this.password = password;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getMobNum() {
		return mobileNumber;
	}

	public void setMobNum(String mobNum) {
		this.mobileNumber = mobNum;
	}

	public String getGovId() {
		return govId;
	}

	public void setGovId(String govId) {
		this.govId = govId;
	}

	public String getDob() {
		return dob;
	}

	public void setDob(String dob) {
		this.dob = dob;
	}

	public String getEmail() {
		return emailId;
	}

	public void setEmail(String email) {
		this.emailId = email;
	}

	public String getPassword() {
		return password;
	}

	public void setPassword(String password) {
		this.password = password;
	}

	public List<Travels> getFlightBookings() {	
		return travels;
	}    
        
        
        
        
 OUTPUT:

1.Register
2.Login
3.Exit
1
enter name:
Jaheera Shaik
enter mobilenumber:
9541582365
enter govidNum:
25452336523
enter dob(DD/MM/YYYY):
28/07/1999
enter emailId:
shaikjaheera@gmail.com
enter Password:
786325

1.Register
2.Login
3.Exit
2
Enter MobileNumber:
9541582365
Enter Password:
786325

1.BookTicket
2.History
3.Exit
1
From...
vijayawada
To
hyderabad
no flights found in the route?

1.BookTicket
2.History
3.Exit
1
From...
hyderabad
To
mumbai
1-->ListOfFlights [flightName=Redbus, from=hyderabad, to=mumbai, startTime=13:00, endTime=24:00, price=9900]
1
enter name:
sameena
enter age:
25
booking your ticket...
ticket booked successfully...!


1.BookTicket
2.History
3.Exit
2
Journey [name=sameena, age=25, flightName=Redbus, from=hyderabad, to=mumbai, startTime=13:00, endTime=24:00, price=9900]

1.BookTicket
2.History
3.Exit
3
Logging you out...

1.Register
2.Login
3.Exit
3
Exiting...

  
        
        
        
        
    
