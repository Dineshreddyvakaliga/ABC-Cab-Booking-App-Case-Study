# ABC-Cab-Booking-App-Case-Study
This case study explores data analysis for the ABC Cab-Booking App using SQL queries. The objective is to analyze user rides, driver performance, city partnerships, customer segments, and user complaints to enhance service quality and operational efficiency.
## 📊 Case Study Overview
This repository contains SQL queries to analyze different aspects of the ABC Cab-Booking App, helping the company optimize operations, improve customer satisfaction, and make data-driven decisions.

---

## 🏆 Key Analyses & SQL Queries

### 1️⃣ User Rides and User Information Analysis (FULL JOIN)
🔍 **Goal:** Combine user ride data with user information to understand ride frequency, popular routes, and user preferences.
```sql
SELECT * FROM user_rides UR
FULL JOIN user_information UF
ON UR.user_id = UF.user_id;
```

### 2️⃣ Driver Data and Feedback Analysis (FULL JOIN)
🔍 **Goal:** Understand the correlation between driver performance and customer feedback.
```sql
SELECT * FROM drivers D
FULL JOIN driver_feedback DF
ON D.id = DF.driver_id;
```

### 3️⃣ City Partnerships Exploration (CROSS JOIN)
🔍 **Goal:** Identify potential partnerships and collaborations to enhance customer services.
```sql
SELECT * FROM cities 
CROSS JOIN partner_companies;
```

### 4️⃣ Market Analysis (CROSS JOIN)
🔍 **Goal:** Identify lucrative customer segments in each city for targeted marketing.
```sql
SELECT 
    C.city_name, 
    S.segment_name
FROM cities C
CROSS JOIN customer_segments S;
```

### 5️⃣ Specific User Complaints Analysis (INNER JOIN)
🔍 **Goal:** Retrieve all complaint details for a specific user.
```sql
SELECT 
    UC.complaint_id,
    UF.user_id,
    UF.full_name,
    CC.category_name
FROM user_complaints UC
JOIN user_information UF
ON UC.user_id = UF.user_id
JOIN complaint_category CC
ON UC.category_id = CC.category_id
WHERE UC.user_id = 10115;
```

### 6️⃣ Resolved Cab Complaints Analysis (INNER JOIN)
🔍 **Goal:** Analyze complaints that have been resolved or led to legal action.
```sql
SELECT 
    UC.complaint_id,
    CS.status,
    UC.subcategory_id
FROM complaint_status CS
JOIN user_complaints UC
ON CS.complaint_id = UC.complaint_id
WHERE CS.status = 'resolved' OR CS.status='legal action taken';
```

### 7️⃣ Cab Complaints Report Generation (LEFT JOIN & INNER JOIN)
🔍 **Goal:** Generate a comprehensive report on user complaints, including missing user information.
```sql
SELECT 
    UC.complaint_id,
    UI.full_name,
    UI.email,
    CC.category_name,
    CD.reason
FROM user_complaints UC
LEFT JOIN user_information UI
ON UC.user_id = UI.user_id
INNER JOIN complaint_category CC
ON UC.category_id = CC.category_id
INNER JOIN category_description CD
ON CD.subcategory_id = UC.subcategory_id
ORDER BY UC.complaint_id;
```

### 8️⃣ Identifying Complaint-Free Users (LEFT JOIN)
🔍 **Goal:** Identify users who have never filed a complaint.
```sql
SELECT
    UI.user_id,
    UI.full_name
FROM user_information UI
LEFT JOIN user_complaints UC
ON UI.user_id = UC.user_id
WHERE UC.complaint_id IS NULL;
```

### 9️⃣ User Complaints and Status Analysis (RIGHT JOIN)
🔍 **Goal:** Retrieve distinct complaint IDs with user details and the most recent status.
```sql
SELECT DISTINCT
    CS.complaint_id,
    UC.user_id,
    CS.status,
    MAX(CS.updated)
FROM user_complaints UC
RIGHT JOIN complaint_status CS
ON UC.complaint_id = CS.complaint_id
GROUP BY CS.complaint_id;
```

### 🔟 City-Driver Distribution Analysis (RIGHT JOIN)
🔍 **Goal:** Analyze the distribution of drivers across cities and identify cities without assigned drivers.
```sql
SELECT 
    CT.city_id,
    CT.city_name,
    D.id,
    D.name
FROM drivers D
RIGHT JOIN cities CT
ON CT.city_id = D.city_id;
```

---

## 🚀 Conclusion
By analyzing this dataset, ABC Cab-Booking App can optimize operations, improve driver performance, enhance customer satisfaction, and establish strategic partnerships.

## 📜 License
This project is open-source and can be freely used and modified.

## 👨‍💻 Contributing
Contributors are welcome to enhance queries and add further insights. Feel free to submit pull requests or raise issues!

📩 **For any queries, reach out to us!**

---

🔹 *Happy Querying!* 🔹
