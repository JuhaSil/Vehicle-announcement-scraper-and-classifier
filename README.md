# Vehicle announcement scraper and classifier

Final project for the Building AI course.


## Summary

Scraper to find suitable vehicle announcements from the market as soon as they are published. Very useful for professional vehicle sellers and purchasers who have to follow the market and to find suitable announcements, but also for private person who would like to find the best deals.


## Background

If you want to find best deals from vehicle market, you have to be quick! First one to contact a person who has just announced his/her vehicle on sale, is always close to getting the deal. However, manually crawling through vehicle sales announcements is very time consuming and new announcements appear all the time so you have to be updating the site all the time. Also prices are been changed from time to time and when it happens, vehicle should be re-evaluated. Portals might have search agents available, but usually their amount is limited and functionality is rather simple as well. Would be super useful if there was some automated scraper + classifier for announcements, which would check announcements right after they are published and notify when some vehicle fits the criteria.


## How is it used?

### Creating a search

User is able to set parameters for announcements he/she is willing to find

* Location (Max distance to point X)
* Brand, Model and Type of vehicle (for example "Toyota", "Corolla" and "1.6 Terra 5d")
* Body type (Sedan, Hatchback, Estate, SUV...)
* Fuel type (Petrol, Diesel, Electric, Hybrid [Chargeable Petrol, Chargeable Diesel, Non-chargeable Petrol, Non-chargeable Diesel], E85, Gas, Hydrogen)
* Drivetrain (AWD, FWD, RWD)
* Transmission (Automatic, Manual)
* Mileage (Min KM, Max KM)
* Yearmodel (Min KM, Max KM)
* Price (Min €, Max €, VAT included or not)
* Cylinder volume (Min, Max)
* Power (Min kW, Max kW)
* Co2 emissions (Max co2)
* Etc.
* Possibility to add almost any filter and AI would get a hold of it? Like searching for some exact equipment, color, interior, etc.

### Classifying results

After finding a suitable vehicle, it would be also important to compare the asking price to similar vehicles on the market and give a commercial score for it.

  * We would have to run certain corrections to the price to see how it compares to other similar vehicles. Some vehicle might seem
    cheap, but it has a lot of defects and when those are taken also into account, price is even higher than other similar vehicles:
  
      * Is there a full service history? How does it affect the price?
      * Does it have damages that are told on announcement? How could we estimate the cost to fix them?
      * Are there two sets (or even more) of tyres? Bigger summer wheels and car is looking REALLY nice?
      * Does vehicle have some special equipment? Could it lift the price? What are those equipment?
      
  * How does price compare to importing a similar car from other market?
    
      * Remember to count also VAT differences, transport costs, local taxes (for example car tax in Finland), registration costs...
      * It is always easier to sell a car which is already on local market, but this information is important to avoid risks.
      * If import price is way cheaper than local price -> Big risk that local prices are coming down rapidly or consumers end up purchasing their vehicles from abroad.
      * Import prices are a lot higher than local prices -> Possibility to export the vehicle?

  * After comparing to current market, we should also check the sales history of similar vehicles:

      * Is there a pattern which kind of units were sold the fastest?
      * And from which location? Differences in prices or sales times in different areas?
      * Some colours / interiors are worse / better to sell than others?
      * VAT deductible vehicles sell better than others?
      
  * If there are not enough units to compare to, we should widen the search:
    
      * How about +/- 1 yearmodel if model of that exact vehicle type doesn't change?
      * Little more mileage allowed?
      * Some other brand has a sister model to compare to?
        
  * It is possible to give a price rating based on these different facts. -> Notification to user if rating is above the set limit


## Data sources

Data would come example from vehicle sales portals. They might also have data about sold vehicles, but most of the times that data is only for commercial users who pay for it. There are also some operators who collect data and sell it for car dealers etc. (for example Netwheels in Finland). Maybe this program could also follow announcements when vehicles are published and/or sold? So we could get information on sales times, price history + price when sold... Of cource we still wouldn't know if seller gave discount or not, but at least we would know the asking price when vehicle left the market. There is also data available about vehicles with their VIN number: You are able to get for example technical and equipment information for most brands. Also local vehicle register data is available with VIN or register number of the car.


## AI Methods

Multiple different methods could be used:

* **Nearest neighbour**  //  Find closest vehicles to compare to
* **Neural networks**  //  Defining the price estimation based on vehicle data + market data + history data.
  

## Challenges

Used vehicles are always individuals. Estimating all the costs and overall commerciality of a vehicle can be very hard. 

For example if you have a car which is worth 20.000€ when it's in good condition but has an engine failure and new engine would cost 15.000€ to install -> Price of this car might still be 12.000€ and not 5.000€ in it's current condition. So not all costs can be count totally off the price. In this case, paying 8000€ for the vehicle would be a bargain, but program would estimate it to be worth 5.000€.

Some equipment are deal breakers. For example some vehicles can only have a towing hook installed in factory as new. Retrofitting a hook is not possible. This of cource will cause those vehicles with towing hook to be a lot more valuable than the others. Or Mercedes-Benz S-class has a special "Executive Business package" worth 50.000€ as new -> Can we even closely compare it to same kind of vehicles which don't have that equipment? List price of this vehicle is like 200.000€ when others are 150.000€ -> Should it be also now more expensive in same ratio compared to others or is this equipment only worth 50% anymore?
