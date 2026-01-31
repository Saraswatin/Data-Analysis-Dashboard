# Ola-Analysis-Dashboard
Cleaned and processed data from multiple sources, performed analysis using SQL queries, and visualized key trends in Power BI dashboards, resulting in a 10% reduction in cancellation rate by implementing optimized business strategies.
use ola;
-- 1. Retrieve all successful bookings:
	
    create View Successfull_bookings as 
    select * from bookings where Booking_Status='success';
    
-- 2. Find the average ride distance for each vehicle type:

	create View  RideDistance AS
	select Vehicle_Type, AVG(Ride_Distance) as Average_ridedistance from bookings Group by Vehicle_Type;
	
-- 3. Get the total number of cancelled rides by customers:

	Create View Cancelled_Ride_Customers as
	select count(*) from bookings where Booking_Status='Canceled by Customer';
	
-- 4. List the top 5 customers who booked the highest number of rides:

	Create View Top_5_Customers as
	select Customer_ID, count(Booking_ID) as Total_Rides
    from bookings
    Group By Customer_ID 
    Order By Total_Rides limit 5;
	
-- 5. Get the number of rides cancelled by drivers due to personal and car-related issues:

	Create View Drive_Cancelled_By_Drivers_P_C_Cancelled as
	select count(*) from bookings 
    where Canceled_Rides_by_Driver='Personal & Car related issue';
	
-- 6. Find the maximum and minimum driver ratings for Prime Sedan bookings:

	create View  MAX_MIN_Ratings_Drivers as
	select Max(Driver_Ratings) as Max_Ratings ,Min(Driver_Ratings) as Min_Ratings from bookings;
	
-- 7. Retrieve all rides where payment was made using UPI:

	create View UPI_Payments as
	select * from bookings where Payment_Method='UPI';
	
-- 8. Find the average customer rating per vehicle type:

	create View Avg_Customer_Ratings as
    select AVG(Customer_Rating),Vehicle_Type from bookings Group by Vehicle_Type;
	
-- 9. Calculate the total booking value of rides completed successfully:
	 
     create View Total_Bookings_successfull as
     select count(Booking_Status) from bookings where Booking_Status='success';
	 
-- 10. List all incomplete rides along with the reason
	
    create View Incomplete_rides as
	select Incomplete_Rides,Incomplete_Rides_Reason from bookings  where Incomplete_Rides='yes';
