# -DeepQuery
Diving into Subqueries &amp; Views for Advanced SQL

This project delves into the power of subqueries and views in SQL, exploring how they enhance data retrieval, optimize performance, and simplify complex queries. Through practical examples and real-world use cases, we aim to demonstrate best practices for writing efficient subqueries and leveraging views for better database management. 

1. Find the number of persons in each country
   
      select country_name, count(Id) as PersonCount from Persons where country_name is not null group by country_name order by country_name;
   
2. Find the number of persons in each country sorted from high to low.

      select country_name, count(Id) as PersonCount from Persons where country_name is not null group by country_name order by PersonCount desc;

3. Find out an average rating for Persons in respective countries if the average is greater than 3.0.

      select Fname, avg(rating) as AvgRating, Country_name from Persons group by country_name,Fname having AvgRating>3.0;

4. Find the countries with the same rating as the USA.

   select distinct(country_name)  from Persons where Rating =(select distinct(Rating) from Persons where country_name='USA')
   
5.Select all countries whose population is greater than the average population of all nations.

    select country_name from country where population> (select avg(population) from country  );

Create a database named Product and create a table called Customer with the following fields in the Product database: Customer_Id - Make PRIMARY KEY First_name Last_name Email Phone_no Address City State Zip_code Country 

    create database Product;
    
    USE Product;
    
    create table Customer  
    
      (
      
	      Customer_Id INT primary key,
       
        First_name varchar(50) NOT NULL,
        
        Last_name varchar(50) NOT NULL,
        
        Email varchar(200) UNIQUE NOT NULL,
        
        Phone_no varchar(20) UNIQUE NOT NULL,
        
        Address varchar(200),
        
        City varchar(100),
        
        State varchar(100),
        
        Zip_code varchar(100),
        
        Country varchar(25)
        
      );	

   1. Create a view named customer_info for the Customer table that displays Customer’s Full name and email address.
      
      create view customer_info as select concat(First_name,' ',Last_name) as Fullname, Email from Customer;

      select * from customer_info;

  2. Create a view named US_Customers that displays customers located in the US.

     create view US_Customers as 
     select Customer_Id, First_name, Last_name, Email, Phone_no, Address, City, State, Zip_code, Country
     from Customer where Country = 'USA';

     select * from US_Customers;

  3. Create another view named Customer_details with columns full name(Combine first_name and last_name), email, phone_no, and state.

     create view Customer_details as 
     select concat(First_name,' ',Last_name) as Fullname, Email, Phone_no,  State from Customer;

     select * from Customer_details;

  5. Update phone numbers of customers who live in California for Customer_details view.

     set sql_safe_updates =0;
      update Customer
      set Phone_no = '234-567-8909'  
        where State = 'CA';
6. Count the number of customers in each state and show only states with more than 5 customers.

   select State, COUNT(Customer_Id) AS Customer_Count from Customer group by State having COUNT(Customer_Id) > 5;
   
7. Write a query that will return the number of customers in each state, based on the "state" column in the "customer_details" view.

    select State, COUNT(*) as Customer_Count from Customer_details group by State;

8. Write a query that returns all the columns from the "customer_details" view, sorted by the "state" column in ascending order.

    select * from Customer_details order by State asc;
  
   

     

     
      

       
   
