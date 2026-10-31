# StrataScratch PySpark Interview Questions Master Repository

Welcome to the definitive collection of **PySpark Interview Questions from StrataScratch**, formatted as structured, modular Markdown guides for Data Engineers, Data Scientists, and Big Data Analysts.

Every question contains the full problem statement, input schemas, sample data previews, step-by-step interview strategy, idiomatic **PySpark DataFrame API solution**, alternative **PySpark SQL solution**, and performance optimization notes.

---

## 📊 Repository Statistics

| Metric | Count | Description |
| :--- | :--- | :--- |
| **Total Coding Challenges** | **139** | Real-world interview questions scraped from StrataScratch |
| 🟢 **Easy Problems** | **32** | Foundational DataFrames, filtering, basic group-bys |
| 🟡 **Medium Problems** | **47** | Window functions, multi-table joins, date math, text parsing |
| 🔴 **Hard Problems** | **60** | Complex window framing, retention rates, consecutive sequences, self-joins |
| 📘 **Theory & Architecture Guides** | **6** | In-depth guides covering Catalyst, Tungsten, Shuffling, Joins, Memory |

---

## 📁 Repository Structure

```text
P:\Pyspark\
├── README.md                                  # Master index and PySpark cheat-sheet
├── 01_Easy\                                   # 32 Easy-level interview questions
├── 02_Medium\                                 # 47 Medium-level interview questions
├── 03_Hard\                                   # 60 Hard-level interview questions
└── 04_PySpark_Theory_Concepts\                # Core architecture & theory interview guides
    ├── 01_Spark_Architecture_and_Execution_Model.md
    ├── 02_Transformations_vs_Actions_and_Lazy_Evaluation.md
    ├── 03_Catalyst_Optimizer_and_Tungsten_Engine.md
    ├── 04_Shuffling_Partitioning_and_Memory_Management.md
    ├── 05_Join_Strategies_Broadcast_vs_SortMerge.md
    └── 06_Window_Functions_and_Complex_Aggregations.md
```

---

## 📘 PySpark Core Theory & Architecture Guides

Essential reading for senior data engineering technical rounds:

1. [**01. Spark Architecture & Execution Model**](04_PySpark_Theory_Concepts/01_Spark_Architecture_and_Execution_Model.md) - Driver, Executors, Cluster Managers, Py4J Bridge, Jobs, Stages, and Tasks.
2. [**02. Transformations vs. Actions & Lazy Evaluation**](04_PySpark_Theory_Concepts/02_Transformations_vs_Actions_and_Lazy_Evaluation.md) - Narrow vs. Wide dependencies, DAG compilation, Lineage graph, fault recovery.
3. [**03. Catalyst Optimizer & Project Tungsten**](04_PySpark_Theory_Concepts/03_Catalyst_Optimizer_and_Tungsten_Engine.md) - 4-stage optimization, predicate pushdown, projection pruning, off-heap memory, WSCG.
4. [**04. Shuffling, Partitioning & Memory Management**](04_PySpark_Theory_Concepts/04_Shuffling_Partitioning_and_Memory_Management.md) - Shuffle mechanics, `repartition` vs. `coalesce`, data skew, key salting, Spark unified memory pool.
5. [**05. Join Strategies: Broadcast vs. Sort-Merge**](04_PySpark_Theory_Concepts/05_Join_Strategies_Broadcast_vs_SortMerge.md) - Broadcast Hash Join (BHJ), Sort-Merge Join (SMJ), Shuffle Hash Join (SHJ), Cartesian joins.
6. [**06. Window Functions & Complex Aggregations**](04_PySpark_Theory_Concepts/06_Window_Functions_and_Complex_Aggregations.md) - Window framing (`rowsBetween` vs. `rangeBetween`), `dense_rank` vs. `rank`, `lead` / `lag`, rolling averages.

---

## 🏢 Questions by Company Tag

<details>
<summary><b>Click to expand questions by Company (15 Companies)</b></summary>


### Tech Industry (73 Questions)
- [`[2000]` **Variable Vs Fixed Rates**](03_Hard/2000_variable_vs_fixed_rates.md) — *Hard* (Data Transformation & Analytics)
- [`[2001]` **Share Of Loan Balance**](01_Easy/2001_share_of_loan_balance.md) — *Easy* (Window Functions & Ranking)
- [`[2002]` **Submission Types**](03_Hard/2002_submission_types.md) — *Hard* (Data Transformation & Analytics)
- [`[2003]` **Recent Refinance Submissions**](03_Hard/2003_recent_refinance_submissions.md) — *Hard* (Joins & Relational Data)
- [`[2012]` **Viewers Turned Streamers**](03_Hard/2012_viewers_turned_streamers.md) — *Hard* (Data Transformation & Analytics)
- [`[2018]` **Inactive Free Users**](03_Hard/2018_inactive_free_users.md) — *Hard* (Date & Time Analytics)
- [`[2019]` **Top 2 Users With Most Calls**](03_Hard/2019_top_2_users_with_most_calls.md) — *Hard* (Data Transformation & Analytics)
- [`[2024]` **Unique Users Per Client Per Month**](01_Easy/2024_unique_users_per_client_per_month.md) — *Easy* (Aggregations & Grouping)
- [`[2029]` **Most Popular Client For Calls**](03_Hard/2029_most_popular_client_for_calls.md) — *Hard* (Joins & Relational Data)
- [`[2032]` **Signups By Billing Cycle**](02_Medium/2032_signups_by_billing_cycle.md) — *Medium* (Joins & Relational Data)
- [`[2033]` **Find The Most Profitable Location**](03_Hard/2033_find_the_most_profitable_location.md) — *Hard* (Data Transformation & Analytics)
- [`[2039]` **Products Report Summary**](02_Medium/2039_products_report_summary.md) — *Medium* (Joins & Relational Data)
- [`[2050]` **Daily Active Users**](01_Easy/2050_daily_active_users.md) — *Easy* (Aggregations & Grouping)
- [`[2051]` **Monthly Active Users**](02_Medium/2051_monthly_active_users.md) — *Medium* (Aggregations & Grouping)
- [`[2058]` **Total Shipment Weight**](01_Easy/2058_total_shipment_weight.md) — *Easy* (Window Functions & Ranking)
- [`[2059]` **Player With Longest Streak**](03_Hard/2059_player_with_longest_streak.md) — *Hard* (Date & Time Analytics)
- [`[2060]` **Manager Of The Largest Department**](03_Hard/2060_manager_of_the_largest_department.md) — *Hard* (Data Transformation & Analytics)
- [`[2072]` **Active Users Per Platform**](01_Easy/2072_active_users_per_platform.md) — *Easy* (Aggregations & Grouping)
- [`[2075]` **Homework Results**](03_Hard/2075_homework_results.md) — *Hard* (Data Transformation & Analytics)
- [`[2097]` **Premium Accounts**](02_Medium/2097_premium_accounts.md) — *Medium* (Joins & Relational Data)
- [`[2099]` **Election Results**](02_Medium/2099_election_results.md) — *Medium* (Joins & Relational Data)
- [`[2102]` **Flags Per Video**](02_Medium/2102_flags_per_video.md) — *Medium* (Aggregations & Grouping)
- [`[2104]` **User With Most Approved Flags**](02_Medium/2104_user_with_most_approved_flags.md) — *Medium* (Joins & Relational Data)
- [`[2125]` **Process A Refund**](02_Medium/2125_process_a_refund.md) — *Medium* (Joins & Relational Data)
- [`[2126]` **Account Registrations**](02_Medium/2126_account_registrations.md) — *Medium* (Aggregations & Grouping)
- [`[2150]` **Customers Who Purchased The Same Product**](02_Medium/2150_customers_who_purchased_the_same_product.md) — *Medium* (Joins & Relational Data)
- [`[2160]` **Oregon's Prior Month's Sales**](01_Easy/2160_oregon_s_prior_month_s_sales.md) — *Easy* (Joins & Relational Data)
- [`[9610]` **Find Students At Median Writing**](02_Medium/9610_find_students_at_median_writing.md) — *Medium* (Date & Time Analytics)
- [`[9613]` **Find The Date With The Highest Opening Stock Price**](02_Medium/9613_find_the_date_with_the_highest_opening_stock_price.md) — *Medium* (Aggregations & Grouping)
- [`[9614]` **Find The Average Difference Between Booking And Check-in Dates**](01_Easy/9614_find_the_average_difference_between_booking_and_ch.md) — *Easy* (Aggregations & Grouping)
- [`[9615]` **Solo Apartment Search**](01_Easy/9615_solo_apartment_search.md) — *Easy* (Aggregations & Grouping)
- [`[9650]` **Top 10 Songs 2010**](02_Medium/9650_top_10_songs_2010.md) — *Medium* (Date & Time Analytics)
- [`[9653]` **Macbookpro User Event Count**](01_Easy/9653_macbookpro_user_event_count.md) — *Easy* (Aggregations & Grouping)
- [`[9669]` **Count The Number Of Speakers Per Each Language**](01_Easy/9669_count_the_number_of_speakers_per_each_language.md) — *Easy* (Joins & Relational Data)
- [`[9672]` **Count The Unique Origin Airports**](01_Easy/9672_count_the_unique_origin_airports.md) — *Easy* (Data Transformation & Analytics)
- [`[9680]` **Most Profitable Companies**](03_Hard/9680_most_profitable_companies.md) — *Hard* (Data Transformation & Analytics)
- [`[9712]` **Find The First And Last Times The Maximum Score Was Awarded**](02_Medium/9712_find_the_first_and_last_times_the_maximum_score_wa.md) — *Medium* (Aggregations & Grouping)
- [`[9762]` **Find The Day Of The Week That Most People Check In**](02_Medium/9762_find_the_day_of_the_week_that_most_people_check_in.md) — *Medium* (Aggregations & Grouping)
- [`[9782]` **Customer Revenue In March**](02_Medium/9782_customer_revenue_in_march.md) — *Medium* (Aggregations & Grouping)
- [`[9845]` **April Admin Employees**](01_Easy/9845_april_admin_employees.md) — *Easy* (Joins & Relational Data)
- [`[9847]` **Workers By Department Since April**](01_Easy/9847_workers_by_department_since_april.md) — *Easy* (Joins & Relational Data)
- [`[9870]` **Highest Salary**](02_Medium/9870_highest_salary.md) — *Medium* (Aggregations & Grouping)
- [`[9881]` **Titanic Survivors And Non-survivors**](02_Medium/9881_titanic_survivors_and_non_survivors.md) — *Medium* (Joins & Relational Data)
- [`[9892]` **Second Highest Salary**](02_Medium/9892_second_highest_salary.md) — *Medium* (Window Functions & Ranking)
- [`[9895]` **Duplicate Emails**](01_Easy/9895_duplicate_emails.md) — *Easy* (Aggregations & Grouping)
- [`[9897]` **Highest Salary In Department**](03_Hard/9897_highest_salary_in_department.md) — *Hard* (Joins & Relational Data)
- [`[9900]` **Median Salary**](03_Hard/9900_median_salary.md) — *Hard* (Data Transformation & Analytics)
- [`[9908]` **Customer Orders And Details**](03_Hard/9908_customer_orders_and_details.md) — *Hard* (Data Transformation & Analytics)
- [`[9909]` **Highest Number Of Orders**](02_Medium/9909_highest_number_of_orders.md) — *Medium* (Joins & Relational Data)
- [`[9913]` **Order Details**](01_Easy/9913_order_details.md) — *Easy* (Joins & Relational Data)
- [`[9915]` **Highest Cost Orders**](01_Easy/9915_highest_cost_orders.md) — *Easy* (Joins & Relational Data)
- [`[9924]` **Email Preference Missing**](01_Easy/9924_email_preference_missing.md) — *Easy* (Aggregations & Grouping)
- [`[10005]` **Hour Of Highest Gas Expense**](01_Easy/10005_hour_of_highest_gas_expense.md) — *Easy* (Aggregations & Grouping)
- [`[10006]` **Find The Averag Distance Traveled In Each Hour**](01_Easy/10006_find_the_averag_distance_traveled_in_each_hour.md) — *Easy* (Aggregations & Grouping)
- [`[10026]` **Aroma-based Winery Search.**](03_Hard/10026_aroma_based_winery_search.md) — *Hard* (Aggregations & Grouping)
- [`[10042]` **Top 3 Wineries In The World**](03_Hard/10042_top_3_wineries_in_the_world.md) — *Hard* (String & Text Processing)
- [`[10128]` **Abigail Breslin Nominations**](01_Easy/10128_abigail_breslin_nominations.md) — *Easy* (Date & Time Analytics)
- [`[10148]` **Find The Top 5 Cities With The Most 5 Star Businesses**](03_Hard/10148_find_the_top_5_cities_with_the_most_5_star_busines.md) — *Hard* (Window Functions & Ranking)
- [`[10161]` **Ranking Hosts By Beds**](02_Medium/10161_ranking_hosts_by_beds.md) — *Medium* (Window Functions & Ranking)
- [`[10164]` **Total Adwords Earnings**](01_Easy/10164_total_adwords_earnings.md) — *Easy* (Aggregations & Grouping)
- [`[10167]` **Total Number Of Housing Units**](01_Easy/10167_total_number_of_housing_units.md) — *Easy* (Date & Time Analytics)
- [`[10170]` **Gende With Most Doctor Appointments**](01_Easy/10170_gende_with_most_doctor_appointments.md) — *Easy* (Aggregations & Grouping)
- [`[10172]` **Best Selling Item**](03_Hard/10172_best_selling_item.md) — *Hard* (Joins & Relational Data)
- [`[10176]` **Bikes Last Used**](01_Easy/10176_bikes_last_used.md) — *Easy* (Aggregations & Grouping)
- [`[10183]` **Total Cost Of Orders**](01_Easy/10183_total_cost_of_orders.md) — *Easy* (Joins & Relational Data)
- [`[10283]` **Find The Top-ranked Songs For The Past 30 Years.**](02_Medium/10283_find_the_top_ranked_songs_for_the_past_30_years.md) — *Medium* (Date & Time Analytics)
- [`[10303]` **Top Percentile Fraud**](03_Hard/10303_top_percentile_fraud.md) — *Hard* (Window Functions & Ranking)
- [`[10308]` **Salaries Differences**](01_Easy/10308_salaries_differences.md) — *Easy* (Joins & Relational Data)
- [`[10310]` **Class Performance**](03_Hard/10310_class_performance.md) — *Hard* (Data Transformation & Analytics)
- [`[10315]` **Cities With The Most Expensive Homes**](02_Medium/10315_cities_with_the_most_expensive_homes.md) — *Medium* (Filtering & Conditional Logic)
- [`[10318]` **New Products**](02_Medium/10318_new_products.md) — *Medium* (Joins & Relational Data)
- [`[10353]` **Workers With The Highest Salaries**](01_Easy/10353_workers_with_the_highest_salaries.md) — *Easy* (Joins & Relational Data)
- [`[10354]` **Most Profitable Companies**](03_Hard/10354_most_profitable_companies.md) — *Hard* (Data Transformation & Analytics)

### Meta / Facebook (20 Questions)
- [`[2004]` **Number Of Comments Per User In Past 30 Days**](03_Hard/2004_number_of_comments_per_user_in_past_30_days.md) — *Hard* (Data Transformation & Analytics)
- [`[2005]` **Share Of Active Users**](03_Hard/2005_share_of_active_users.md) — *Hard* (Aggregations & Grouping)
- [`[2006]` **Users Activity Per Month Day**](01_Easy/2006_users_activity_per_month_day.md) — *Easy* (Aggregations & Grouping)
- [`[2007]` **Rank Variance Per Country**](03_Hard/2007_rank_variance_per_country.md) — *Hard* (Filtering & Conditional Logic)
- [`[2062]` **Questions In Second Quarter**](03_Hard/2062_questions_in_second_quarter.md) — *Hard* (Data Transformation & Analytics)
- [`[9781]` **Processed Ticket Rate By Type**](02_Medium/9781_processed_ticket_rate_by_type.md) — *Medium* (Joins & Relational Data)
- [`[9791]` **Views Per Keyword**](03_Hard/9791_views_per_keyword.md) — *Hard* (Data Transformation & Analytics)
- [`[10046]` **Top 5 States With 5 Star Businesses**](03_Hard/10046_top_5_states_with_5_star_businesses.md) — *Hard* (Window Functions & Ranking)
- [`[10049]` **Reviews Of Categories**](02_Medium/10049_reviews_of_categories.md) — *Medium* (Aggregations & Grouping)
- [`[10061]` **Popularity Of Hack**](01_Easy/10061_popularity_of_hack.md) — *Easy* (Date & Time Analytics)
- [`[10065]` **Find Whether The Number Of Seniors Works At Meta Facebook**](02_Medium/10065_find_whether_the_number_of_seniors_works_at_meta_f.md) — *Medium* (Joins & Relational Data)
- [`[10087]` **Find All Posts Which Were Reacted To With A Heart**](02_Medium/10087_find_all_posts_which_were_reacted_to_with_a_heart.md) — *Medium* (Joins & Relational Data)
- [`[10134]` **Spam Posts**](02_Medium/10134_spam_posts.md) — *Medium* (Data Transformation & Analytics)
- [`[10284]` **Popularity Percentage**](03_Hard/10284_popularity_percentage.md) — *Hard* (Aggregations & Grouping)
- [`[10285]` **Acceptance Rate By Date**](02_Medium/10285_acceptance_rate_by_date.md) — *Medium* (Joins & Relational Data)
- [`[10295]` **Most Active Users On Messenger**](03_Hard/10295_most_active_users_on_messenger.md) — *Hard* (Data Transformation & Analytics)
- [`[10296]` **Meta/facebook Accounts**](02_Medium/10296_meta_facebook_accounts.md) — *Medium* (Aggregations & Grouping)
- [`[10297]` **Comments Distribution**](03_Hard/10297_comments_distribution.md) — *Hard* (Joins & Relational Data)
- [`[10352]` **Users By Average Session Time**](03_Hard/10352_users_by_average_session_time.md) — *Hard* (Window Functions & Ranking)
- [`[10548]` **Top Actor Ratings By Genre**](03_Hard/10548_top_actor_ratings_by_genre.md) — *Hard* (Window Functions & Ranking)

### Airbnb (9 Questions)
- [`[9624]` **Accommodates-to-bed Ratio**](03_Hard/9624_accommodates_to_bed_ratio.md) — *Hard* (Date & Time Analytics)
- [`[9628]` **Reviews Bins On Reviews Number**](03_Hard/9628_reviews_bins_on_reviews_number.md) — *Hard* (Date & Time Analytics)
- [`[9632]` **Host Popularity Rental Prices**](02_Medium/9632_host_popularity_rental_prices.md) — *Medium* (Aggregations & Grouping)
- [`[9633]` **City With Most Amenities**](03_Hard/9633_city_with_most_amenities.md) — *Hard* (Aggregations & Grouping)
- [`[9636]` **Cheapest Neighborhoods With Real Beds And Internet**](03_Hard/9636_cheapest_neighborhoods_with_real_beds_and_internet.md) — *Hard* (Filtering & Conditional Logic)
- [`[9642]` **Find The Number Of Unique Properties**](03_Hard/9642_find_the_number_of_unique_properties.md) — *Hard* (Data Transformation & Analytics)
- [`[10073]` **Favorite Host Nationality**](02_Medium/10073_favorite_host_nationality.md) — *Medium* (Data Transformation & Analytics)
- [`[10078]` **Matching Similar Hosts And Guests**](02_Medium/10078_matching_similar_hosts_and_guests.md) — *Medium* (Joins & Relational Data)
- [`[10159]` **Ranking Most Active Guests**](02_Medium/10159_ranking_most_active_guests.md) — *Medium* (Window Functions & Ranking)

### Salesforce (8 Questions)
- [`[2052]` **User Growth Rate**](03_Hard/2052_user_growth_rate.md) — *Hard* (Data Transformation & Analytics)
- [`[2053]` **Retention Rate**](03_Hard/2053_retention_rate.md) — *Hard* (Window Functions & Ranking)
- [`[2054]` **Consecutive Days**](03_Hard/2054_consecutive_days.md) — *Hard* (Window Functions & Ranking)
- [`[2063]` **Change Of Currency Exchange Rates**](03_Hard/2063_change_of_currency_exchange_rates.md) — *Hard* (Date & Time Analytics)
- [`[9905]` **Highest Target Under Manager**](01_Easy/9905_highest_target_under_manager.md) — *Easy* (Aggregations & Grouping)
- [`[10077]` **Income By Title And Gender**](02_Medium/10077_income_by_title_and_gender.md) — *Medium* (Joins & Relational Data)
- [`[10182]` **Number Of Streets Per Zip Code**](02_Medium/10182_number_of_streets_per_zip_code.md) — *Medium* (Aggregations & Grouping)
- [`[10319]` **Monthly Percentage Difference**](03_Hard/10319_monthly_percentage_difference.md) — *Hard* (Window Functions & Ranking)

### Google (7 Questions)
- [`[9794]` **Words With Two Vowels**](03_Hard/9794_words_with_two_vowels.md) — *Hard* (Data Transformation & Analytics)
- [`[9814]` **Counting Instances In Text**](03_Hard/9814_counting_instances_in_text.md) — *Hard* (Aggregations & Grouping)
- [`[9817]` **Count Occurrences Of Words In Drafts**](02_Medium/9817_count_occurrences_of_words_in_drafts.md) — *Medium* (Date & Time Analytics)
- [`[9818]` **File Contents Shuffle**](03_Hard/9818_file_contents_shuffle.md) — *Hard* (Data Transformation & Analytics)
- [`[9823]` **Common Letters**](03_Hard/9823_common_letters.md) — *Hard* (Data Transformation & Analytics)
- [`[10068]` **User Email Labels**](02_Medium/10068_user_email_labels.md) — *Medium* (Data Transformation & Analytics)
- [`[10351]` **Activity Rank**](02_Medium/10351_activity_rank.md) — *Medium* (Window Functions & Ranking)

### Amazon (4 Questions)
- [`[2057]` **Weight For First Shipment**](03_Hard/2057_weight_for_first_shipment.md) — *Hard* (Date & Time Analytics)
- [`[2136]` **Customer Tracking**](03_Hard/2136_customer_tracking.md) — *Hard* (Window Functions & Ranking)
- [`[10322]` **Finding User Purchases**](02_Medium/10322_finding_user_purchases.md) — *Medium* (Window Functions & Ranking)
- [`[10553]` **Finding Purchases**](02_Medium/10553_finding_purchases.md) — *Medium* (Window Functions & Ranking)

### Lyft (3 Questions)
- [`[2079]` **City With Most Customers**](03_Hard/2079_city_with_most_customers.md) — *Hard* (Filtering & Conditional Logic)
- [`[10004]` **Find All Lyft Rides Which Happened On Rainy Days Before Noon**](01_Easy/10004_find_all_lyft_rides_which_happened_on_rainy_days_b.md) — *Easy* (Date & Time Analytics)
- [`[10324]` **Distances Traveled**](03_Hard/10324_distances_traveled.md) — *Hard* (Data Transformation & Analytics)

### Microsoft (3 Questions)
- [`[10299]` **Finding Updated Records**](01_Easy/10299_finding_updated_records.md) — *Easy* (Window Functions & Ranking)
- [`[10300]` **Premium Vs Freemium**](02_Medium/10300_premium_vs_freemium.md) — *Medium* (Joins & Relational Data)
- [`[10301]` **Expensive Projects**](03_Hard/10301_expensive_projects.md) — *Hard* (Data Transformation & Analytics)

### DoorDash (2 Questions)
- [`[2035]` **Avg Order Cost During Rush Hours**](03_Hard/2035_avg_order_cost_during_rush_hours.md) — *Hard* (Date & Time Analytics)
- [`[2036]` **Lowest Revenue Generated Restaurants**](03_Hard/2036_lowest_revenue_generated_restaurants.md) — *Hard* (Filtering & Conditional Logic)

### Uber (2 Questions)
- [`[2049]` **Total Order Per Status Per Service**](03_Hard/2049_total_order_per_status_per_service.md) — *Hard* (Data Transformation & Analytics)
- [`[10302]` **Distance Per Dollar**](03_Hard/10302_distance_per_dollar.md) — *Hard* (Date & Time Analytics)

### LinkedIn (2 Questions)
- [`[2055]` **Average Customers Per City**](03_Hard/2055_average_customers_per_city.md) — *Hard* (Data Transformation & Analytics)
- [`[10304]` **Risky Projects**](03_Hard/10304_risky_projects.md) — *Hard* (Data Transformation & Analytics)

### Netflix (2 Questions)
- [`[2163]` **Sorting Movies By Duration Time**](02_Medium/2163_sorting_movies_by_duration_time.md) — *Medium* (Date & Time Analytics)
- [`[10171]` **Find The Genre Of The Person With The Most Number Of Oscar Winnings**](03_Hard/10171_find_the_genre_of_the_person_with_the_most_number_.md) — *Hard* (Joins & Relational Data)

### City of Los Angeles (2 Questions)
- [`[10090]` **Find The Percentage Of Shipable Orders**](02_Medium/10090_find_the_percentage_of_shipable_orders.md) — *Medium* (Window Functions & Ranking)
- [`[10142]` **No Order Customers**](02_Medium/10142_no_order_customers.md) — *Medium* (Joins & Relational Data)

### ESPN (1 Questions)
- [`[9942]` **Largest Olympics**](03_Hard/9942_largest_olympics.md) — *Hard* (Aggregations & Grouping)

### Yelp (1 Questions)
- [`[10060]` **Top Cool Votes**](02_Medium/10060_top_cool_votes.md) — *Medium* (Data Transformation & Analytics)

</details>

---

## 🎯 Questions by Category / Pattern

<details>
<summary><b>Click to expand questions by Pattern & Topic ({len(categories)} Categories)</b></summary>


### Joins & Relational Data (33 Questions)
- [`[2003]` **Recent Refinance Submissions**](03_Hard/2003_recent_refinance_submissions.md) — *Hard* (Tech Industry)
- [`[2029]` **Most Popular Client For Calls**](03_Hard/2029_most_popular_client_for_calls.md) — *Hard* (Tech Industry)
- [`[2032]` **Signups By Billing Cycle**](02_Medium/2032_signups_by_billing_cycle.md) — *Medium* (Tech Industry)
- [`[2039]` **Products Report Summary**](02_Medium/2039_products_report_summary.md) — *Medium* (Tech Industry)
- [`[2097]` **Premium Accounts**](02_Medium/2097_premium_accounts.md) — *Medium* (Tech Industry)
- [`[2099]` **Election Results**](02_Medium/2099_election_results.md) — *Medium* (Tech Industry)
- [`[2104]` **User With Most Approved Flags**](02_Medium/2104_user_with_most_approved_flags.md) — *Medium* (Tech Industry)
- [`[2125]` **Process A Refund**](02_Medium/2125_process_a_refund.md) — *Medium* (Tech Industry)
- [`[2150]` **Customers Who Purchased The Same Product**](02_Medium/2150_customers_who_purchased_the_same_product.md) — *Medium* (Tech Industry)
- [`[2160]` **Oregon's Prior Month's Sales**](01_Easy/2160_oregon_s_prior_month_s_sales.md) — *Easy* (Tech Industry)
- [`[9669]` **Count The Number Of Speakers Per Each Language**](01_Easy/9669_count_the_number_of_speakers_per_each_language.md) — *Easy* (Tech Industry)
- [`[9781]` **Processed Ticket Rate By Type**](02_Medium/9781_processed_ticket_rate_by_type.md) — *Medium* (Meta / Facebook)
- [`[9845]` **April Admin Employees**](01_Easy/9845_april_admin_employees.md) — *Easy* (Tech Industry)
- [`[9847]` **Workers By Department Since April**](01_Easy/9847_workers_by_department_since_april.md) — *Easy* (Tech Industry)
- [`[9881]` **Titanic Survivors And Non-survivors**](02_Medium/9881_titanic_survivors_and_non_survivors.md) — *Medium* (Tech Industry)
- [`[9897]` **Highest Salary In Department**](03_Hard/9897_highest_salary_in_department.md) — *Hard* (Tech Industry)
- [`[9909]` **Highest Number Of Orders**](02_Medium/9909_highest_number_of_orders.md) — *Medium* (Tech Industry)
- [`[9913]` **Order Details**](01_Easy/9913_order_details.md) — *Easy* (Tech Industry)
- [`[9915]` **Highest Cost Orders**](01_Easy/9915_highest_cost_orders.md) — *Easy* (Tech Industry)
- [`[10065]` **Find Whether The Number Of Seniors Works At Meta Facebook**](02_Medium/10065_find_whether_the_number_of_seniors_works_at_meta_f.md) — *Medium* (Meta / Facebook)
- [`[10077]` **Income By Title And Gender**](02_Medium/10077_income_by_title_and_gender.md) — *Medium* (Salesforce)
- [`[10078]` **Matching Similar Hosts And Guests**](02_Medium/10078_matching_similar_hosts_and_guests.md) — *Medium* (Airbnb)
- [`[10087]` **Find All Posts Which Were Reacted To With A Heart**](02_Medium/10087_find_all_posts_which_were_reacted_to_with_a_heart.md) — *Medium* (Meta / Facebook)
- [`[10142]` **No Order Customers**](02_Medium/10142_no_order_customers.md) — *Medium* (City of Los Angeles)
- [`[10171]` **Find The Genre Of The Person With The Most Number Of Oscar Winnings**](03_Hard/10171_find_the_genre_of_the_person_with_the_most_number_.md) — *Hard* (Netflix)
- [`[10172]` **Best Selling Item**](03_Hard/10172_best_selling_item.md) — *Hard* (Tech Industry)
- [`[10183]` **Total Cost Of Orders**](01_Easy/10183_total_cost_of_orders.md) — *Easy* (Tech Industry)
- [`[10285]` **Acceptance Rate By Date**](02_Medium/10285_acceptance_rate_by_date.md) — *Medium* (Meta / Facebook)
- [`[10297]` **Comments Distribution**](03_Hard/10297_comments_distribution.md) — *Hard* (Meta / Facebook)
- [`[10300]` **Premium Vs Freemium**](02_Medium/10300_premium_vs_freemium.md) — *Medium* (Microsoft)
- [`[10308]` **Salaries Differences**](01_Easy/10308_salaries_differences.md) — *Easy* (Tech Industry)
- [`[10318]` **New Products**](02_Medium/10318_new_products.md) — *Medium* (Tech Industry)
- [`[10353]` **Workers With The Highest Salaries**](01_Easy/10353_workers_with_the_highest_salaries.md) — *Easy* (Tech Industry)

### Aggregations & Grouping (33 Questions)
- [`[2005]` **Share Of Active Users**](03_Hard/2005_share_of_active_users.md) — *Hard* (Meta / Facebook)
- [`[2006]` **Users Activity Per Month Day**](01_Easy/2006_users_activity_per_month_day.md) — *Easy* (Meta / Facebook)
- [`[2024]` **Unique Users Per Client Per Month**](01_Easy/2024_unique_users_per_client_per_month.md) — *Easy* (Tech Industry)
- [`[2050]` **Daily Active Users**](01_Easy/2050_daily_active_users.md) — *Easy* (Tech Industry)
- [`[2051]` **Monthly Active Users**](02_Medium/2051_monthly_active_users.md) — *Medium* (Tech Industry)
- [`[2072]` **Active Users Per Platform**](01_Easy/2072_active_users_per_platform.md) — *Easy* (Tech Industry)
- [`[2102]` **Flags Per Video**](02_Medium/2102_flags_per_video.md) — *Medium* (Tech Industry)
- [`[2126]` **Account Registrations**](02_Medium/2126_account_registrations.md) — *Medium* (Tech Industry)
- [`[9613]` **Find The Date With The Highest Opening Stock Price**](02_Medium/9613_find_the_date_with_the_highest_opening_stock_price.md) — *Medium* (Tech Industry)
- [`[9614]` **Find The Average Difference Between Booking And Check-in Dates**](01_Easy/9614_find_the_average_difference_between_booking_and_ch.md) — *Easy* (Tech Industry)
- [`[9615]` **Solo Apartment Search**](01_Easy/9615_solo_apartment_search.md) — *Easy* (Tech Industry)
- [`[9632]` **Host Popularity Rental Prices**](02_Medium/9632_host_popularity_rental_prices.md) — *Medium* (Airbnb)
- [`[9633]` **City With Most Amenities**](03_Hard/9633_city_with_most_amenities.md) — *Hard* (Airbnb)
- [`[9653]` **Macbookpro User Event Count**](01_Easy/9653_macbookpro_user_event_count.md) — *Easy* (Tech Industry)
- [`[9712]` **Find The First And Last Times The Maximum Score Was Awarded**](02_Medium/9712_find_the_first_and_last_times_the_maximum_score_wa.md) — *Medium* (Tech Industry)
- [`[9762]` **Find The Day Of The Week That Most People Check In**](02_Medium/9762_find_the_day_of_the_week_that_most_people_check_in.md) — *Medium* (Tech Industry)
- [`[9782]` **Customer Revenue In March**](02_Medium/9782_customer_revenue_in_march.md) — *Medium* (Tech Industry)
- [`[9814]` **Counting Instances In Text**](03_Hard/9814_counting_instances_in_text.md) — *Hard* (Google)
- [`[9870]` **Highest Salary**](02_Medium/9870_highest_salary.md) — *Medium* (Tech Industry)
- [`[9895]` **Duplicate Emails**](01_Easy/9895_duplicate_emails.md) — *Easy* (Tech Industry)
- [`[9905]` **Highest Target Under Manager**](01_Easy/9905_highest_target_under_manager.md) — *Easy* (Salesforce)
- [`[9924]` **Email Preference Missing**](01_Easy/9924_email_preference_missing.md) — *Easy* (Tech Industry)
- [`[9942]` **Largest Olympics**](03_Hard/9942_largest_olympics.md) — *Hard* (ESPN)
- [`[10005]` **Hour Of Highest Gas Expense**](01_Easy/10005_hour_of_highest_gas_expense.md) — *Easy* (Tech Industry)
- [`[10006]` **Find The Averag Distance Traveled In Each Hour**](01_Easy/10006_find_the_averag_distance_traveled_in_each_hour.md) — *Easy* (Tech Industry)
- [`[10026]` **Aroma-based Winery Search.**](03_Hard/10026_aroma_based_winery_search.md) — *Hard* (Tech Industry)
- [`[10049]` **Reviews Of Categories**](02_Medium/10049_reviews_of_categories.md) — *Medium* (Meta / Facebook)
- [`[10164]` **Total Adwords Earnings**](01_Easy/10164_total_adwords_earnings.md) — *Easy* (Tech Industry)
- [`[10170]` **Gende With Most Doctor Appointments**](01_Easy/10170_gende_with_most_doctor_appointments.md) — *Easy* (Tech Industry)
- [`[10176]` **Bikes Last Used**](01_Easy/10176_bikes_last_used.md) — *Easy* (Tech Industry)
- [`[10182]` **Number Of Streets Per Zip Code**](02_Medium/10182_number_of_streets_per_zip_code.md) — *Medium* (Salesforce)
- [`[10284]` **Popularity Percentage**](03_Hard/10284_popularity_percentage.md) — *Hard* (Meta / Facebook)
- [`[10296]` **Meta/facebook Accounts**](02_Medium/10296_meta_facebook_accounts.md) — *Medium* (Meta / Facebook)

### Data Transformation & Analytics (31 Questions)
- [`[2000]` **Variable Vs Fixed Rates**](03_Hard/2000_variable_vs_fixed_rates.md) — *Hard* (Tech Industry)
- [`[2002]` **Submission Types**](03_Hard/2002_submission_types.md) — *Hard* (Tech Industry)
- [`[2004]` **Number Of Comments Per User In Past 30 Days**](03_Hard/2004_number_of_comments_per_user_in_past_30_days.md) — *Hard* (Meta / Facebook)
- [`[2012]` **Viewers Turned Streamers**](03_Hard/2012_viewers_turned_streamers.md) — *Hard* (Tech Industry)
- [`[2019]` **Top 2 Users With Most Calls**](03_Hard/2019_top_2_users_with_most_calls.md) — *Hard* (Tech Industry)
- [`[2033]` **Find The Most Profitable Location**](03_Hard/2033_find_the_most_profitable_location.md) — *Hard* (Tech Industry)
- [`[2049]` **Total Order Per Status Per Service**](03_Hard/2049_total_order_per_status_per_service.md) — *Hard* (Uber)
- [`[2052]` **User Growth Rate**](03_Hard/2052_user_growth_rate.md) — *Hard* (Salesforce)
- [`[2055]` **Average Customers Per City**](03_Hard/2055_average_customers_per_city.md) — *Hard* (LinkedIn)
- [`[2060]` **Manager Of The Largest Department**](03_Hard/2060_manager_of_the_largest_department.md) — *Hard* (Tech Industry)
- [`[2062]` **Questions In Second Quarter**](03_Hard/2062_questions_in_second_quarter.md) — *Hard* (Meta / Facebook)
- [`[2075]` **Homework Results**](03_Hard/2075_homework_results.md) — *Hard* (Tech Industry)
- [`[9642]` **Find The Number Of Unique Properties**](03_Hard/9642_find_the_number_of_unique_properties.md) — *Hard* (Airbnb)
- [`[9672]` **Count The Unique Origin Airports**](01_Easy/9672_count_the_unique_origin_airports.md) — *Easy* (Tech Industry)
- [`[9680]` **Most Profitable Companies**](03_Hard/9680_most_profitable_companies.md) — *Hard* (Tech Industry)
- [`[9791]` **Views Per Keyword**](03_Hard/9791_views_per_keyword.md) — *Hard* (Meta / Facebook)
- [`[9794]` **Words With Two Vowels**](03_Hard/9794_words_with_two_vowels.md) — *Hard* (Google)
- [`[9818]` **File Contents Shuffle**](03_Hard/9818_file_contents_shuffle.md) — *Hard* (Google)
- [`[9823]` **Common Letters**](03_Hard/9823_common_letters.md) — *Hard* (Google)
- [`[9900]` **Median Salary**](03_Hard/9900_median_salary.md) — *Hard* (Tech Industry)
- [`[9908]` **Customer Orders And Details**](03_Hard/9908_customer_orders_and_details.md) — *Hard* (Tech Industry)
- [`[10060]` **Top Cool Votes**](02_Medium/10060_top_cool_votes.md) — *Medium* (Yelp)
- [`[10068]` **User Email Labels**](02_Medium/10068_user_email_labels.md) — *Medium* (Google)
- [`[10073]` **Favorite Host Nationality**](02_Medium/10073_favorite_host_nationality.md) — *Medium* (Airbnb)
- [`[10134]` **Spam Posts**](02_Medium/10134_spam_posts.md) — *Medium* (Meta / Facebook)
- [`[10295]` **Most Active Users On Messenger**](03_Hard/10295_most_active_users_on_messenger.md) — *Hard* (Meta / Facebook)
- [`[10301]` **Expensive Projects**](03_Hard/10301_expensive_projects.md) — *Hard* (Microsoft)
- [`[10304]` **Risky Projects**](03_Hard/10304_risky_projects.md) — *Hard* (LinkedIn)
- [`[10310]` **Class Performance**](03_Hard/10310_class_performance.md) — *Hard* (Tech Industry)
- [`[10324]` **Distances Traveled**](03_Hard/10324_distances_traveled.md) — *Hard* (Lyft)
- [`[10354]` **Most Profitable Companies**](03_Hard/10354_most_profitable_companies.md) — *Hard* (Tech Industry)

### Window Functions & Ranking (19 Questions)
- [`[2001]` **Share Of Loan Balance**](01_Easy/2001_share_of_loan_balance.md) — *Easy* (Tech Industry)
- [`[2053]` **Retention Rate**](03_Hard/2053_retention_rate.md) — *Hard* (Salesforce)
- [`[2054]` **Consecutive Days**](03_Hard/2054_consecutive_days.md) — *Hard* (Salesforce)
- [`[2058]` **Total Shipment Weight**](01_Easy/2058_total_shipment_weight.md) — *Easy* (Tech Industry)
- [`[2136]` **Customer Tracking**](03_Hard/2136_customer_tracking.md) — *Hard* (Amazon)
- [`[9892]` **Second Highest Salary**](02_Medium/9892_second_highest_salary.md) — *Medium* (Tech Industry)
- [`[10046]` **Top 5 States With 5 Star Businesses**](03_Hard/10046_top_5_states_with_5_star_businesses.md) — *Hard* (Meta / Facebook)
- [`[10090]` **Find The Percentage Of Shipable Orders**](02_Medium/10090_find_the_percentage_of_shipable_orders.md) — *Medium* (City of Los Angeles)
- [`[10148]` **Find The Top 5 Cities With The Most 5 Star Businesses**](03_Hard/10148_find_the_top_5_cities_with_the_most_5_star_busines.md) — *Hard* (Tech Industry)
- [`[10159]` **Ranking Most Active Guests**](02_Medium/10159_ranking_most_active_guests.md) — *Medium* (Airbnb)
- [`[10161]` **Ranking Hosts By Beds**](02_Medium/10161_ranking_hosts_by_beds.md) — *Medium* (Tech Industry)
- [`[10299]` **Finding Updated Records**](01_Easy/10299_finding_updated_records.md) — *Easy* (Microsoft)
- [`[10303]` **Top Percentile Fraud**](03_Hard/10303_top_percentile_fraud.md) — *Hard* (Tech Industry)
- [`[10319]` **Monthly Percentage Difference**](03_Hard/10319_monthly_percentage_difference.md) — *Hard* (Salesforce)
- [`[10322]` **Finding User Purchases**](02_Medium/10322_finding_user_purchases.md) — *Medium* (Amazon)
- [`[10351]` **Activity Rank**](02_Medium/10351_activity_rank.md) — *Medium* (Google)
- [`[10352]` **Users By Average Session Time**](03_Hard/10352_users_by_average_session_time.md) — *Hard* (Meta / Facebook)
- [`[10548]` **Top Actor Ratings By Genre**](03_Hard/10548_top_actor_ratings_by_genre.md) — *Hard* (Meta / Facebook)
- [`[10553]` **Finding Purchases**](02_Medium/10553_finding_purchases.md) — *Medium* (Amazon)

### Date & Time Analytics (17 Questions)
- [`[2018]` **Inactive Free Users**](03_Hard/2018_inactive_free_users.md) — *Hard* (Tech Industry)
- [`[2035]` **Avg Order Cost During Rush Hours**](03_Hard/2035_avg_order_cost_during_rush_hours.md) — *Hard* (DoorDash)
- [`[2057]` **Weight For First Shipment**](03_Hard/2057_weight_for_first_shipment.md) — *Hard* (Amazon)
- [`[2059]` **Player With Longest Streak**](03_Hard/2059_player_with_longest_streak.md) — *Hard* (Tech Industry)
- [`[2063]` **Change Of Currency Exchange Rates**](03_Hard/2063_change_of_currency_exchange_rates.md) — *Hard* (Salesforce)
- [`[2163]` **Sorting Movies By Duration Time**](02_Medium/2163_sorting_movies_by_duration_time.md) — *Medium* (Netflix)
- [`[9610]` **Find Students At Median Writing**](02_Medium/9610_find_students_at_median_writing.md) — *Medium* (Tech Industry)
- [`[9624]` **Accommodates-to-bed Ratio**](03_Hard/9624_accommodates_to_bed_ratio.md) — *Hard* (Airbnb)
- [`[9628]` **Reviews Bins On Reviews Number**](03_Hard/9628_reviews_bins_on_reviews_number.md) — *Hard* (Airbnb)
- [`[9650]` **Top 10 Songs 2010**](02_Medium/9650_top_10_songs_2010.md) — *Medium* (Tech Industry)
- [`[9817]` **Count Occurrences Of Words In Drafts**](02_Medium/9817_count_occurrences_of_words_in_drafts.md) — *Medium* (Google)
- [`[10004]` **Find All Lyft Rides Which Happened On Rainy Days Before Noon**](01_Easy/10004_find_all_lyft_rides_which_happened_on_rainy_days_b.md) — *Easy* (Lyft)
- [`[10061]` **Popularity Of Hack**](01_Easy/10061_popularity_of_hack.md) — *Easy* (Meta / Facebook)
- [`[10128]` **Abigail Breslin Nominations**](01_Easy/10128_abigail_breslin_nominations.md) — *Easy* (Tech Industry)
- [`[10167]` **Total Number Of Housing Units**](01_Easy/10167_total_number_of_housing_units.md) — *Easy* (Tech Industry)
- [`[10283]` **Find The Top-ranked Songs For The Past 30 Years.**](02_Medium/10283_find_the_top_ranked_songs_for_the_past_30_years.md) — *Medium* (Tech Industry)
- [`[10302]` **Distance Per Dollar**](03_Hard/10302_distance_per_dollar.md) — *Hard* (Uber)

### Filtering & Conditional Logic (5 Questions)
- [`[2007]` **Rank Variance Per Country**](03_Hard/2007_rank_variance_per_country.md) — *Hard* (Meta / Facebook)
- [`[2036]` **Lowest Revenue Generated Restaurants**](03_Hard/2036_lowest_revenue_generated_restaurants.md) — *Hard* (DoorDash)
- [`[2079]` **City With Most Customers**](03_Hard/2079_city_with_most_customers.md) — *Hard* (Lyft)
- [`[9636]` **Cheapest Neighborhoods With Real Beds And Internet**](03_Hard/9636_cheapest_neighborhoods_with_real_beds_and_internet.md) — *Hard* (Airbnb)
- [`[10315]` **Cities With The Most Expensive Homes**](02_Medium/10315_cities_with_the_most_expensive_homes.md) — *Medium* (Tech Industry)

### String & Text Processing (1 Questions)
- [`[10042]` **Top 3 Wineries In The World**](03_Hard/10042_top_3_wineries_in_the_world.md) — *Hard* (Tech Industry)

</details>

---

## 📑 Complete Master Problem Index

| ID | Title | Difficulty | Company | Category | Solution Link |
| :---: | :--- | :---: | :--- | :--- | :---: |
| `2000` | **Variable Vs Fixed Rates** | 🔴 `Hard` | Tech Industry | Data Transformation & Analytics | [View Solution](03_Hard/2000_variable_vs_fixed_rates.md) |
| `2001` | **Share Of Loan Balance** | 🟢 `Easy` | Tech Industry | Window Functions & Ranking | [View Solution](01_Easy/2001_share_of_loan_balance.md) |
| `2002` | **Submission Types** | 🔴 `Hard` | Tech Industry | Data Transformation & Analytics | [View Solution](03_Hard/2002_submission_types.md) |
| `2003` | **Recent Refinance Submissions** | 🔴 `Hard` | Tech Industry | Joins & Relational Data | [View Solution](03_Hard/2003_recent_refinance_submissions.md) |
| `2004` | **Number Of Comments Per User In Past 30 Days** | 🔴 `Hard` | Meta / Facebook | Data Transformation & Analytics | [View Solution](03_Hard/2004_number_of_comments_per_user_in_past_30_days.md) |
| `2005` | **Share Of Active Users** | 🔴 `Hard` | Meta / Facebook | Aggregations & Grouping | [View Solution](03_Hard/2005_share_of_active_users.md) |
| `2006` | **Users Activity Per Month Day** | 🟢 `Easy` | Meta / Facebook | Aggregations & Grouping | [View Solution](01_Easy/2006_users_activity_per_month_day.md) |
| `2007` | **Rank Variance Per Country** | 🔴 `Hard` | Meta / Facebook | Filtering & Conditional Logic | [View Solution](03_Hard/2007_rank_variance_per_country.md) |
| `2012` | **Viewers Turned Streamers** | 🔴 `Hard` | Tech Industry | Data Transformation & Analytics | [View Solution](03_Hard/2012_viewers_turned_streamers.md) |
| `2018` | **Inactive Free Users** | 🔴 `Hard` | Tech Industry | Date & Time Analytics | [View Solution](03_Hard/2018_inactive_free_users.md) |
| `2019` | **Top 2 Users With Most Calls** | 🔴 `Hard` | Tech Industry | Data Transformation & Analytics | [View Solution](03_Hard/2019_top_2_users_with_most_calls.md) |
| `2024` | **Unique Users Per Client Per Month** | 🟢 `Easy` | Tech Industry | Aggregations & Grouping | [View Solution](01_Easy/2024_unique_users_per_client_per_month.md) |
| `2029` | **Most Popular Client For Calls** | 🔴 `Hard` | Tech Industry | Joins & Relational Data | [View Solution](03_Hard/2029_most_popular_client_for_calls.md) |
| `2032` | **Signups By Billing Cycle** | 🟡 `Medium` | Tech Industry | Joins & Relational Data | [View Solution](02_Medium/2032_signups_by_billing_cycle.md) |
| `2033` | **Find The Most Profitable Location** | 🔴 `Hard` | Tech Industry | Data Transformation & Analytics | [View Solution](03_Hard/2033_find_the_most_profitable_location.md) |
| `2035` | **Avg Order Cost During Rush Hours** | 🔴 `Hard` | DoorDash | Date & Time Analytics | [View Solution](03_Hard/2035_avg_order_cost_during_rush_hours.md) |
| `2036` | **Lowest Revenue Generated Restaurants** | 🔴 `Hard` | DoorDash | Filtering & Conditional Logic | [View Solution](03_Hard/2036_lowest_revenue_generated_restaurants.md) |
| `2039` | **Products Report Summary** | 🟡 `Medium` | Tech Industry | Joins & Relational Data | [View Solution](02_Medium/2039_products_report_summary.md) |
| `2049` | **Total Order Per Status Per Service** | 🔴 `Hard` | Uber | Data Transformation & Analytics | [View Solution](03_Hard/2049_total_order_per_status_per_service.md) |
| `2050` | **Daily Active Users** | 🟢 `Easy` | Tech Industry | Aggregations & Grouping | [View Solution](01_Easy/2050_daily_active_users.md) |
| `2051` | **Monthly Active Users** | 🟡 `M