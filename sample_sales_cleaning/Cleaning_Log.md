**📑 DATA CLEANING LOG – sales\_data\_clean.xlsx**



Tool Used: Power Query (Power BI / Excel) + Excel Manual Cleaning

Dataset Type: Sales Transaction Fact Table

Rows: 2,800+

Columns: 25+



**🧹 1. IMPORT \& INITIAL INSPECTION**

✔ Loaded original sales\_data\_sample.xlsx

✔ Identified major issues:



Mixed date formats (2/24/2003, 05-07-2003, 07-01-2003 00:00)



Text stored as numbers (postal codes, phone)



Incorrect state values (e.g., "a", "cisco", "me", "N 5804")



Missing postal codes



CITY column inconsistencies (e.g., "Nyc", "cisco", "me")



ADDRESS lines containing "None"



Special character corruption in names (e.g., Mart;n)



Extra spaces \& wrong capitalization



DEAL\_SIZE categories inconsistent



Currency not formatted



PHONE column had symbols, spaces, country codes



🛠 2. POWER QUERY CLEANING STEPS

✔ 2.1 Converted Data Types



ORDER\_DATE → Converted using Using Locale (English - US)



QUANTITY, PRICE\_EACH, SALES → Converted to numeric



POSTALCODE → Forced to Text (important for global data)



✔ 2.2 Trimmed \& Cleaned Whitespaces



Applied:



Trim



Clean



To:

CITY, STATE, POSTALCODE, COUNTRY, TERRITORY, CONTACT NAMES, ADDRESS lines.



✔ 2.3 Fixed ORDER\_DATE



Removed “00:00:00” timestamps



Standardized format to dd-mm-yyyy



Ensured no null/invalid dates



Extracted clean date into ORDER\_DATE\_CLEAN



Removed temporary transformation column



✔ 2.4 Cleaned STATE Column



Identified invalid values:



a, me, cisco, ge, ne, N 5804



Actions:



Correct USA states using CITY reference (NYC → NY, Newark → NJ, etc.)



For non-USA rows → left STATE blank (correct practice)



Moved 5804 from STATE → POSTALCODE (Norway)



✔ 2.5 Cleaned POSTALCODE



Reassigned misplaced postal values



Ensured all global zip formats preserved:



France: 5 digits



Norway: N 5804(old format) changed to new 5804



UK: WX1 6LT



Sweden: S-958 22



Australia: 3004, 2067



Singapore: 79903



Concluded missing US ZIPs cannot be inferred → left blank



✔ 2.6 Cleaned CITY Column



Fixed:



Nyc → NYC



cisco → San Francisco



me → blank



ne → blank



Applied Proper Case to standard city names.



✔ 2.7 Cleaned ADDRESS LINES



Replaced "None" with blank



Trimmed spaces



Converted to Proper Case



Preserved address supplements (“Suite 101”, “Level 6”)



✔ 2.8 Cleaned NAMES



Replaced corrupted characters:



Mart;n → Martin



Proper Case applied to:



CUSTOMER\_NAME



CONTACT\_FIRST\_NAME



CONTACT\_LAST\_NAME



✔ 2.9 Cleaned DEAL\_SIZE



Unified categories:



Small



Medium



Large



✔ 2.10 Cleaned TERRITORY



Standardized to:



NA



EMEA



APAC



✔ 2.11 PHONE Column Fix



Removed special characters



Removed semicolons, brackets, spaces



Normalized all phone numbers to digits only



Kept as text to preserve leading zeroes



✏️ 3. MANUAL EXCEL CLEANING (POST-PQ)

✔ Fixed names with corrupted characters (Mart;n → Martin)

✔ Applied proper casing to city \& names

✔ Aligned all columns:



Text → left



Numbers → right



Dates → center



✔ Applied consistent currency formatting (not typed $)



PRICE\_EACH → Currency (2 decimals)



SALES → Currency (2 decimals)



✔ Auto-fit column widths

✔ Freezed top header row

✔ Checked for accidental nulls / “None” / spaces

✔ Confirmed ORDER\_DATE sorted and correct

🚫 4. DUPLICATES HANDLING



NO duplicate rows removed

Reason:



This dataset is a sales transaction fact table



Duplicate ORDER\_NUMBER values expected (multiple order lines per order)



Only checked for accidental structural duplicates → none found.

5 Conditional formatting applied to DEAL_SIZE
Small- Red
Large- Green

📌 5. FINAL DATA QUALITY STATUS

✔ 100% valid dates

✔ 100% correct country names

✔ 100% cleaned postal codes

✔ All TEXT columns properly standardized

✔ All MONEY columns numeric + currency formatted

✔ Deal Size categories normalized

✔ Address, Phone, Names cleaned

✔ No broken characters

✔ All null/state/city errors fixed

✔ Dataset ready for Power BI, SQL, Analysis

🎯 6. FINAL OUTPUT FILES



Sales_data_clean.xlsx (Final cleaned dataset)



Cleaning_log.md (This log)



Sales_data_raw.xlsx (Raw source)



🧾 7. Summary in 3 Lines 



Performed full data cleaning using Power Query \& Excel: fixed date formats, standardized global postal codes, cleaned names, corrected addresses \& states, normalized text fields, and applied currency formatting.

Ensured accurate order-level sales data without deleting valid duplicates.

Final dataset prepared for analysis, dashboards, and machine learning.

