# Exploratory Data Analysis using Excel

*** 
-- Based on certain keywords, I placed the job titles into four categories namely:
-- Data Scientist
-- Data Analyst
-- Machine Learning
-- Data Engineer
------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the Search, Find, Isnumber and Ifs function to perform multiple logical test which categorises the job titles based on certain keywords
=IFS(
    ISNUMBER(SEARCH("Data Scientist", B2)), "Data Scientist", 
    ISNUMBER(FIND("Computational Behavioral Scientist", B2)), "Data Engineer", 
    ISNUMBER(FIND("Statistics", B2)), "Data Engineer", 
    ISNUMBER(FIND("Computational Scientist", B2)), "Data Engineer", 
    ISNUMBER(FIND("Chief Scientist", B2)), "Machine Learning", 
    ISNUMBER(FIND(" AI", B2)), "Machine Learning", 
    ISNUMBER(SEARCH("Statistical Scientist", B2)), "Data Scientist", 
    ISNUMBER(SEARCH("Data Architect", B2)), "Data Engineer", 
    ISNUMBER(SEARCH("Decision Scientist", B2)), "Data Scientist", 
    ISNUMBER(SEARCH("Analyst", B2)), "Data Analyst", 
    ISNUMBER(FIND("RWE", B2)), "Data Scientist", 
    ISNUMBER(SEARCH("Data Integration and Modeling Engineer", B2)), "Data Engineer", 
    ISNUMBER(SEARCH("Business Intelligence Analyst", B2)), "Data Analyst",  
    ISNUMBER(SEARCH("Data Science", B2)), "Data Scientist", 
    ISNUMBER(SEARCH("Data Analytics", B2)), "Data Analyst",  
    ISNUMBER(SEARCH("Data Analyst", B2)), "Data Analyst",  
    ISNUMBER(SEARCH("Data Engineer", B2)), "Data Engineer", 
    ISNUMBER(SEARCH("Learning", B2)), "Machine Learning", 
    ISNUMBER(SEARCH("Analytics", B2)), "Data Analyst", 
    ISNUMBER(SEARCH("Data Modeler", B2)), "Data Engineer"
    )

---------------------------------------------------------------------------------------------------------------------------------------
--Extracted only the numeric values from the Salary Estimate column
---------------------------------------------------------------------------------------------------------------------------------------
-- I extracted the numeric values using the Mid function
-- I also use the SUBSTITUTE function to remove the '$' and 'k' currency symbols 

=SUBSTITUTE(SUBSTITUTE(MID(F2, 1, FIND("(", F2) - 2), "$", ""), "K", "")

---------------------------------------------------------------------------------------------------------------------------------------
-- I used the Average function to find the Overall Salary Estimate AVG
---------------------------------------------------------------------------------------------------------------------------------------
=AVERAGE(H2:H643)

---------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords, I was able to check if experience is required from the job description column 
---------------------------------------------------------------------------------------------------------------------------------------
-- I used the Search, Isnumber and If function to search for keywords matching "Experience Required" in the Job Desciption Column 
=IF(ISNUMBER(SEARCH("Experience", J2)),  "Experience Required", 0)

---------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if a bachelor's degree is required from the job description column
---------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, OR, ISNUMBER, SEARCH and FIND functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether a Bachelor degree is required or not

=IF(
    OR(
        ISNUMBER(SEARCH("Bachelor's Degree", J2)), 
        ISNUMBER(SEARCH("B.sc", J2)), 
        ISNUMBER(SEARCH("Bachelor", J2)), 
        ISNUMBER(SEARCH("Bsc", J2)), 
        ISNUMBER(SEARCH("MBA", J2)), 
        ISNUMBER(SEARCH("Degree", J2)), 
        ISNUMBER(FIND("BS", J2))
    ),
 "Bsc Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in the formula below, I was able to check if a Master's degree is required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, OR, ISNUMBER, SEARCH and FIND functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether a Master's degree is required or not

 =IF(
    OR(
        ISNUMBER(SEARCH("Master's Degree", J2)), 
        ISNUMBER(SEARCH("M.sc", J2)), 
        ISNUMBER(SEARCH("Msc", J2)), 
        ISNUMBER(SEARCH("M.S", J2)),  
        ISNUMBER(SEARCH("Master of", J2)),  
        ISNUMBER(SEARCH("Master in", J2)), 
        ISNUMBER(FIND("MS", J2))
        ), 
    "Masters Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if a Ph.D is required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, OR, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether a Ph.D is required or not

=IF(
    OR(
        ISNUMBER(SEARCH("PhD", J2)), 
        ISNUMBER(SEARCH("Ph.D", J2))
        ), 
    "Ph.D Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if SQL skills are required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether a SQL skills are required or not

    =IF(ISNUMBER(SEARCH("SQL", J2)),  "SQL Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if Python skills are required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether a Python skills are required or not

=IF(ISNUMBER(SEARCH("Python", J2)),  "Python Required", 0)


--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if R Programming language skills is required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, OR, ISNUMBER and FIND functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether R Programming language skill is required or not

=IF(
    OR(
        ISNUMBER(FIND(" R.", J2)), 
        ISNUMBER(FIND(" R,", J2)), 
        ISNUMBER(FIND(" R ", J2))
        ), 
    "R Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if Scala Programming language skills is required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, OR, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether Scala Programming language skill is required or not

=IF(
    OR(
        ISNUMBER( SEARCH("Scala ",J2)), 
        ISNUMBER( SEARCH("Scala.",J2)), 
        ISNUMBER( SEARCH("Scala,",J2))
        ), 
    "Scala Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if Java Programming language skills is required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether Java Programming language skill is required or not

=IF(ISNUMBER(SEARCH("Java", J2)),  "Java Required", 0)


--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if Microsoft Excel Skills is required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, OR, ISNUMBER and FIND functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether a Microsoft Excel Skills is required or not

=IF(
    OR(
        ISNUMBER(FIND("Excel ", J2)), 
        ISNUMBER(FIND("Excel,", J2)), 
        ISNUMBER(FIND("Excel.", J2)), 
        ISNUMBER(FIND("excel ", J2))
        ), 
    "Excel Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if AWS skills are required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether AWS skills are required or not

=IF(ISNUMBER(SEARCH("AWS", J2)),  "AWS Required", 0)

--------------------------------------------------------------------------------------------------------------------------------------------------------
-- Based on certain keywords as specified in thr formula below, I was able to check if Azure skills are required from the job description column
--------------------------------------------------------------------------------------------------------------------------------------------------------
-- I used the IF, ISNUMBER and SEARCH functions to perform logical tests
-- The logical test checks for certain keywords in each job description to determine whether Azure skills are required or not

=IF(ISNUMBER(SEARCH("AZURE", J2)),  "Azure Required", 0)