# Analyzing Customer Rental Patterns and Preferences Through EDA Approach

## Introduction and Background
- Due to uncertainties, there is a strong need to emphasize the exploration of rental patterns and customer preferences.
- This is crucial for improving customer engagement and will optimize the company’s inventory management.
- A traditional DVD rental store that has transitioned to an online rental service needs to adjust and follow market trend.
- There is a strong shift in consumer behavior towards online media consumption; the implications are still unknown.
- How this affects rental business needs to be studied and understood to help the rental store maximise profits.

![image](https://github.com/OnonaChukwu/RBSter_rental/assets/155753951/559dcda7-1850-4001-b2bc-e9d0112bd940)

## Challenge
- The traditional store faces competitive pressure from streaming platforms and other entertainment services.
- There are difficulties in maintaining customer interest and loyalty in a highly competitive market.

## Motivation
- Urgently needed is a data-driven approach to mitigate challenges
- Understanding the market trends and take the best positions vital.
- Predicting customer behaviors to stay competitive in the market is important.
- Insights are needed to ensure better stock management, targeted marketing campaigns, and improved customer service.

## Aim
- To visualize trends and extract actionable insights about customer preferences and rental patterns.

## Objectives
- Identify the most rented movies.
- Understand rental frequency per customer.
- Analyse rental duration trends.
- Identify peak rental periods.

## Methodology
- I extracted data from the rental customer inventory and film tables in a certain database.
- The PostgreSQL queries I produced fetched me the necessary data based on the following:
    - The frequency of rentals.
    - Associated customer details.
    - Film titles and their respective dates.

**Here is the code**
```sql
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    f.title AS film_title,
    COUNT(r.rental_id) AS rental_count,
    EXTRACT(YEAR FROM r.rental_date) AS rental_year,
    EXTRACT(MONTH FROM r.rental_date) AS rental_month,
    EXTRACT(DAY FROM r.rental_date) AS rental_day
FROM rental r
JOIN inventory i ON r.inventory_id = i.inventory_id
JOIN film f ON i.film_id = f.film_id
JOIN customer c ON r.customer_id = c.customer_id
GROUP BY c.customer_id, f.title, EXTRACT(YEAR FROM r.rental_date), EXTRACT(MONTH FROM r.rental_date), EXTRACT(DAY FROM r.rental_date)
ORDER BY c.customer_id, rental_count DESC;
```
**Procedure** 
- I joined four tables — rental, inventory, film, and customer.
- It consolidated information on which films are being rented by which customers.
- I aimed at aggregating data to count the number of times each film is rented by each customer.
- It was tohelp reveal an idea of popular films and active customers over the involved timeline.
- I included year, month, and day from the rental date to help analyze trends over time (year, month).

## The Four Key Questions
- Identify the five most rented movies.
- Identify the least five rented movies.
- What are the rental frequencies of the five top customers?
- Analyse rental duration trends, what insights are therein?

## [Results](https://public.tableau.com/app/profile/charles.ikenna.nwankwo/viz/Data_driven_rental_decision/5_most_rented)
**Identify the five most rented movies**
![image](https://github.com/OnonaChukwu/RBSter_rental/assets/155753951/9890cf54-14eb-4557-b990-b953cf1e78d7)
**The five most rented films are**:
- Bucket Brotherhood - 34
- Rocketeer Mother – 33
- Ridgemont Submarine – 32
- Grit Clockwork – 32
- Juggler Hardly – 32.

**Identify the five least rented movies**
![image](https://github.com/OnonaChukwu/RBSter_rental/assets/155753951/b9c11b36-88d1-4143-a04e-d20d72eaa9e6)
**The five least rented films are**:
- Mixed Doors – 4
- Train Bunch – 4
- Hardly Rubbers – 4
- Mussolini Spoilers – 5
- Freedom Cleopatra

**What are the rental frequencies of the five top customers?**
![image](https://github.com/OnonaChukwu/RBSter_rental/assets/155753951/0cb36472-02a3-439a-8224-0f42863573db)
**They are listed in the following order**:
- Eleanor Hunt (46)
- Karl Seal (45)
- Clara Shaw (42) = Marcia Dean (42)
- Tammy Sanders (41).

**Analyse rental duration trends, what insights are therein?**
![image](https://github.com/OnonaChukwu/RBSter_rental/assets/155753951/213b0619-c842-4c08-b201-f6b7825fceda)
- Rentals occurred from February to August 2005, with the majority in July and August, and with a sharp decline from September 2005 into February 2006.

## Conclusions
- The top rented movies like Bucket Brotherhood and Rocketeer Mother suggest that certain titles have broad appeal;
      - they attract customers and drive rental volume. Focus on similar movies!
- Movies like Mixed Doors and Train Bunch have significantly lower rental counts;
      - they have less overall appeal. Ignore similar movies.
- Customers such as Eleanor Hunt and Karl Seal are highly loyal customers;
      - endeavor to keep them through compensations and remunerations.
- Rental activity peaks in the summer months, particularly in July and August, and drops off towards the year-end.
- It shows a seasonal pattern that likely correlates with customer vacation times or leisure periods; make lots of movies available in summertime.

## Recommendations
- Focus on enhancing marketing for popular films and develop loyalty programs aimed at frequent renters to maximize engagement.
- Tailor inventory and promotional strategies to align with seasonal rental patterns, boosting demand during peak and off-peak periods.


