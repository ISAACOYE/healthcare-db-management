# Healthcare-db-mgmt-fall-2024 Project
The following Repository contains our project for Healthcare Database Management using openly-sourced data to generate a Database as a proof of concept to further understand the architecture behind designing relational databases
- This database primarily focuses on readings taken from activity data (derived from Empatica E4 accelerometry data) and food_log data to analyze readings taken by a Dexcom G6 glucose monitor
- Other Tables are also included for the sake of cohesion of all of the data given through the website resources which are linked below

## ${\textsf{\color{red}Please refer to the second branch of this repository for further detailed files used in our procedure.}}$



### ER Diagram of the Database
![ER_Diagram_HealthCareDBManagement_JV2244](https://github.com/user-attachments/assets/bbe2edf9-6556-4b08-b716-bc33e6dd87a3)




## Link to the SQL Dump File (stored on google drive)
```bash
https://drive.google.com/file/d/1gMe2Q7fD93vVu4l9xx7BBTWhw7wA_ajE/view?usp=sharing
```

## How to Quickly Load the Database

### In Postgres create a database to store the dump file within if you have not already
 ```bash
 createdb -U [user] [database_name]
  ```
### Run the PG Restore command and assign it as no owner to load the info without a role conflict
 ```bash
 pg_restore -U [user] -d [database_name] --no-owner [filepath_to_SQLdump]
  ```
## Useful Functions You Can Use Right Away

#### Get Participant Activity Data (example below)
- Allows you to obtain activity data associated with the selected participant
- Performs a join with the dexcom based glucose readings within the database to show the associated glucose readings
 ```sql
 SELECT * FROM get_participant_activity_data(2);
  ```

#### Get Participant Food Log Data (example below)
- Allows you to obtain food log data associated with the selected participant
- Performs a join with the dexcom based glucose readings within the database to show the associated glucose readings
- The join is performed based off the nearest dexcom datetime as the foreign key as the food_log does not perfectly align with the glucose data but shows readings very close to similar times
 ```sql
 SELECT * FROM get_participant_food_data(2);
  ```

### Reference:
Cho, P., Kim, J., Bent, B., & Dunn, J. (2023). BIG IDEAs Lab Glycemic Variability and Wearable Device Data (version 1.1.2). PhysioNet. https://doi.org/10.13026/zthx-5212 
