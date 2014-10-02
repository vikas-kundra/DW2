#Data Science Assignment

###**Initial Analysis**
After visually analyzing more than 1000 Rows in LibreOffice Calc, few anomalies which were found in data are

1. Customer_Number_Dealer is not present for various Records
2. County is not present for various records
3. Various Zip Codes which are entered are not correct
4. Wrong value of Mileage is present in few Records(For Instance 2)
5. Part Numbers are not present for Every OpCode(Not Sure Whether this is Anomaly)
6. Vehicle Category missing for every Record

###**Data Extraction**
Even though initial investigation of 1000 records did gave us idea about how data is structured
but to completely investigate And for building understanding for data, whole data file was 
extracted in SQL SERVER 2008.
BULK COPY PROGRAM(BCP) was used for transferring the data From TAB separated file to SQL DB.

#####*REQUIREMENTS*
A dummy table Named Dummy_Table which will hold the dump of  TAB separated File

#####*Commands Used*
bcp DW.dbo.Dummy_Table in “/home/ubuntu/Downloads/DataDocument” -f Char.fmt -S <server_name> -U<user_name> -P<password>

###**Table Break Down**
|DB Column   	|File Column   	|Column Understanding   	|Data Type   	|Hypothesis   	|
|---	|---	|---	|---	|---	|
|Dealer_Id   	|Dealer_Id   	|It represents the id of every Dealer,which is used to uniquely identify them   	|Varchar(8000)   	|   	|
|   RO_Number	| Ro_Number	|It represents the Repair order number which is used to uniquely identify them	|   Varchar(8000)	|   	|
|Ro_Close_Date   	|Ro_Close_Date   	|It represents the closing date of Repair Order   	|Varchar(8000)   	|  | 	
|Customer_Num_Dealer   	|Customer_Num_Dealer   	|It represents the Customer Number given by dealer to Customer   	|Varchar(8000)	|[Customer Num Dealer Hypothesis](#CusNumDeal)   	|
|Customer_Full_Name   	|Customer_Full_Name   	|Depicts the name of Customer   	|Varchar(8000)   	|   	|
|County   	|County   	| Provides the name of County  	|Varchar(8000)   	|   	|
|State   	|State   	| Provides the name of County  	|Varchar(8000)   	|   	|
|Zip   	|Zip   	|Provides the name of County   	|Varchar(8000)   	|   	|
|Standard_Address   	|Standardized_Address   	|Depicts whether the address is Standardized   	|Varchar(8000)   	|   	|
|VIN   	|VIN   	|Represents the Vehicle number   |Varchar(8000)   	|   	|
| Mileage  	|Mileage   	|Depicts the Mileage of vehicle   	|Varchar(8000)   	|   	|
|Technician_Number   	|Technician_Number   	|Id provided to technician by dealers   	|Varchar(8000)   	|   	|
|Op_Codes   	|Op_Codes   	|Operation Code for the various operations   	|Varchar(8000)   	|   	|
|Parts_Amount   	|Parts_Amount   	|Holds the amount of various parts Changed/Upgraded   	|Varchar(8000)   	|   	|
|Labour_Amount   	|Labour_Amount   	|Holds the amount of total Labour employed   |Varchar(8000)   	|   	|
|Parts_Number   	|Parts_Number 	|Description about the parts involved in overall operation   	|Varchar(8000)   	|   	|
|Ro_Total   	|Ro_Total   	|Represents the sum of Customer_Labour_Amount,Customer_Parts_Amount,Customer_Misc_Amount,But following hypothesis does not stand true   	|Varchar(8000)   	|[Ro Hypothesis](#RoTotal)   	|
|Customer_Name_Type   	|Customer_Name_Type   	|Represents the value assigned to Customer by dealer,but following hypothesis showsthat various customers are present having both of 1 and 2    	|Varchar(8000)   	|[Customer Name Type Hypothesis](#CusNameType)  	|
|Ro_Line_Num   	|Ro_Line_Num   	|   	|Varchar(8000)   	|   	|
|Labor_Time   	|Labor_Time   	|Depicts the labor time on every operation   	|Varchar(8000)   	|   	|
|Vehicle_Category   	|Vehicle_Category   	|Provides information about the segment of vehicle   	|Varchar(8000)   	|   	|
|Raw_Dealer_Operation_Code   	|Raw_Dealer_Operation_Code     	|Depicts the Operation code by Dealer,but following hypothesis shows that with change in part number,Raw_Dealer_Operation_Code changes    	|Varchar(8000)   	|[Raw Dealer Operation Code](#RawOpCode)   	|
|Customer_Labor_Amount   	|Customer_Labor_Amount   	|Holds the value of Customer share of Labour amount,but following hypothesis is not true,hence it is not valid for all the data    	|Varchar(8000)   	|[Customer Labour Amount Hypothesis](#CusLabAmo)   	|
|Customer_Parts_Amount   	|Customer_Parts_Amount   	|Holds the value of Customer share of Parts amount,but following hypothesis is not true,hence it is not valid for all the data   	|Varchar(8000)   	|[Customer Parts Amount Hypothesis](#CusParAmo)   	|
|Customer_Misc_Amount   	|Customer_Misc_Amount   	|   	|Varchar(8000)   	|   	|
|Warranty_Parts_Amount   	|Warranty_Parts_Amount   	|Holds the value of Warranty share of Parts amount,but folllowing hypothesis is not true,hence it is not valid for all the data   	|Varchar(8000)   	| [Warranty Parts Amount Hypothesis](#WarrParAmo)  	|
|Warranty_Labor_Amount   	|Warranty_Labor_Amount   	| Holds the value of Warranty share of Labour amount,but following hypothesis is not true,hence it is not valid for all the data  	|Varchar(8000)   	|[Warranty Labour Amount Hypothesis](#WarrLabAmo)   	|
|Warranty_Misc_Amount   	|Warranty_Misc_Amount   	|   	|Varchar(8000)   	|   	|
|Internal_Labor_Amount   	|Internal_Labor_Amount   	|Holds the value of that amount which is not included in Labour_Amount and Warranty_Labour,but following hypothesis is not true,hence it is not valid for all the data   	|Varchar(8000)   	|[Internal Labour Amount Hypothesis](#IntLabAmo)   	|
|Internal_Parts_Amount   	|Internal_Parts_Amount   	|Holds the value of that amount which is not included in Labour_Parts and Warranty_Parts,but following hypothesis is not true,hence it is not valid for all the data   	|Varchar(8000)   	|[Internal Parts Amount Hypothesis](#IntParAmo)   	|
|Internal_Misc_Amount   	|Internal_Misc_Amount   	|   	|Varchar(8000)   	|   	|
|Email_Address   	|Email_Address   	|Holds the information of the email address of customer   	|Varchar(8000)   	|   	|
|Model_Year   	|Model_Year   	|Holds the information of year in which vehicle was manufactured   	|Varchar(8000)   	|   	|
|Make_Name   	|Make_Name   	|Holds the information of the maunfacturer of vehicle   	|Varchar(8000)   	|   	|
|Customer_First_Name   	|Customer_First_Name   	|Holds the first name of customer   	|Varchar(8000)   	|   	|
|Customer_Last_Name   	|Customer_Last_Name   	|Holds the last name of customer   	|Varchar(8000)   	|   	|
|Description_1   	|Description_1   	|Describes about the operations performed   	|Varchar(8000)   	|   	|
|Description_2   	|Description_2   	|Provides Additional Details of operation Performed   	|Varchar(8000)   	|[Description Hupothesis](#Description)   	|
|Labor_Per_Op   	|Labor_Per_Op   	|   	|Varchar(8000)   	|   	|
|Parts_Per_Op   	|Parts_Per_Op   	|   	|Varchar(8000)   	|   	|
|FileName   	|FileName   	|   	|Varchar(8000)   	|   	|
|File_Mtime   	|File_Mtime   	|Provides the details about the last time when file was modified   	|Varchar(8000)   	|   	|
|   	|   	|   	|Varchar(8000)   	|   	|
|   	|   	|   	|Varchar(8000)   	|   	|




###**Observation And Encoding**
On Analysing table after dump, it was found that 1 row was missing in the Database.In order to find out that row Dealer_Id and Ro_Number were exported from table Dummy_Table in file ServerDB.Dealer Id and Ro Number were also imported from TAB separated file using awk command in file LocalDB.After that both files were sorted and compared with **DIFF** command, it was found that row having **Dealer Id=51018** and **Ro Number='18079875'** was missing.On analysing that row, it was detected that it was the presence of non Ascii character at the end of Description 2 which prevented TAB for getting detected.


####*Character Encoding*
On further analysing File For Non ASCII Characters using Command  

**LC_ALL=c grep --color='auto' -P -n "[\x80-\xFF]" RO_Example.tab>Output_File**

it was concluded that 59 rows have non ASCII Characters and on searching those rows in DB,it was found that '?' was present in places of those characters.

Non Ascii Characters

1. -
2. ‡
3. ï

####*Solution*
Command “file -bi Output_File” gave output charset=unknown 8 bit,So in order for DB to render these characters, they should be converted to UTF-8

#####*Using Iconv Command*
iconv -f “ascii” -t “utf-8” Output_File>Converted_File

Output:illegal input sequence at position 498

Thus in order to decode this file, some other encoding has to be chosen.Since this file was being rendered clearly by Sublime-Text,Preferences of Sublime Text was observed ,and it was deduced that default option of Sublime text encoding is Windows-1252

**iconv -f “windows-1252” -t “utf-8” Output_File>Converted_File**

On Counting Number Of rows of Converted_File,only 16 rows were Obtained

####Python Script:

    import codecs 
    BLOCKSIZE = 1048576 # or some other, desired size in bytes 
    with codecs.open("Output_File", "r","windows 1252") as sourceFile: 
        with codecs.open("Converted_File" ,"w", "utf-8") as targetFile: 
            while True:
                contents = sourceFile.read(BLOCKSIZE) 
                if not contents: 
                break 
                targetFile.write(contents)```
            
Using Above Python Script,Converted_File Contains 59 rows, and it can be further used for transferring those records in DB,so that they can be rendered Properly.
            
###**HYPOTHESIS AND VALIDATIONS**

#####1. *Hypothesis to be proven is  Ro_Number can Be Primary Key*

**Validating Hypothesis**

    Select Count(Distinct Ro_Number) from Dummy Table

`Output Obtained =768107`

`Total Records Present =1857537`

**41.358%** data Suggests that Ro_Number is unique.Rest of the data did not satisfy this relation, which is even less than half of the total data present,Hence this hypothesis cannot be used while using this data .Hence this hypothesis is false.


#####2. *Hypothesis to be proven is Customer_Num_Dealer is Unique Throughout*


**Validating Hypothesis**

    Select Count(Distinct Customer_Num_Dealer) from Dummy Table

`Output Obtained =372602` 

`Total Records Present =1857537`

Nearly **20.0588%**  of the data have unique Customer_Num_Dealer .So if only that much amount of data is taken for consideration, only then this hypothesis would be true, otherwise based on above result, this hypothesis is false. 

######3. *Hypothesis to be proven is Technician Data is Not Consistent*

**Validating Hypothesis**

*Requirements:*

A table which will hold The Distinct Value of All The Technician_Numbers

    Create Table #NumberTech2
    (
    TECH_NAME VARCHAR(8000)
    )

    Insert Into #NumberTech2 
    
        Select  Distinct(i.items)
    
        From Dummy Table t1
    
        Outer Apply dbo.split(t1.Technician_Number, '^')i  
    
        Order by i.items

    select COUNT(*) as Total_Present from #NumberTech2 

`Total_Present=2450`

    select COUNT(*) as Total_Obtained 

    From #NumberTech2 

    Where ISNUMERIC(TECH_NAME)=0

`Total_Obtained=238`

Almost **9.714%** of the Technician_Number is not.Since this amount cannot be ignored and in order to further strengthen above fact, we would find out that whether all the VARCHAR Technician_Number is not restricted to only 1 or 2 Dealer, which would prove that it is not a typing mistake

    Select Count(Distinct Dealer_Id) as Dealer_Tech_Varchar  

    From Dummy Table 

    Where Technician_Number in(Select * 
                            
                                From #NumberTech2 
                            
                                Where ISNUMERIC(TECH_NAME)=0)

    Select 

    COUNT(Distinct Dealer_Id) as Total_Dealers 

    from Dummy Table

Output Obtained

`Dealer_Tech_Varchar=20`

`Total_Dealers=96`

Thus,Almost **20.833 %** of dealers Technician_Number consists of varchar, which is not confined to only 1 or 2 Dealer.Hence we can conclude from above Observation that, presence of characters in Technician_Number does not prove that data is inconsistent.Hence above Hypothesis has been proved false.

#####4.<a name="LabAndPart"></a> *Hypothesis to be proven is Parts_Amount And Labour_Amount Is Split Up in Customer,Internal And Warranty Parts*

*Requirements:*

A Dummy table Which contains all the fields corresponding To Amount.

    Create Table Amount_Fields_Table
    
    (
    
    Parts_Amount float,
    
    Labour_Amount float,
    
    Ro_Total float,
    
    Cus_Lab_Amount Float,
    
    Cut_Par_Amount float,
    
    Cust_Mis_Amount float,
    
    Warr_Labou_Amount float,
    
    Warr_Parts_Amount float ,
    
    Warr_Miss_Amount float,
    
    Inter_Labour_Amount float,
    
    Inter_Parts_Amount float,
    
    Inter_Misc float
    
    )



Validating Hypothesis

    a)Select * 
    From Amount_Fields_Table 
    Where Cus_Lab_Amount+Inter_Labour_Amount+Warr_Labou_Amount=Labour_Amount


    Select @@ROWCOUNT as Total_Values

`Output Obtained =1660592`

Only 89.3975% of records satisfy above Result.

When above column are *Cast*

    Select * 
    From Amount_Fields_Table
    where Cast(Cus_Lab_Amount as int)+cast(Inter_Labour_Amount as int)+Cast(Warr_Labou_Amount as int)=Cast(Labour_Amount as int)

    Select @@ROWCOUNT as Total_Values

`Total_Values=1752789`

Which is **94.3609%** of the total records.Though this result is better than the previous result, but sill it is not statistically close enough to prove that this relation exists throughout the data.Thus above hypothesis is false

Another point in Favour of proving this hypothesis false is

    Select 
    Count(Distinct(Dealer_Id)) 
    From Amount_Fields_Table 
    Where (Cast(Cus_Lab_Amount as int)+Cast(Inter_Labour_Amount as int)+Cast(Warr_Labou_Amount as int))!=Cast(Labour_Amount as int)

`Output Obtained =93`

Hence almost **96.875%** of the dealers contain data, which does not satisfy above result


    b)Select * 
    from Amount_Fields_Table 
    where
    Cus_Par_Amount +Inter_Parts_Amount +Warr_Parts_Amount=Parts_Amount

    Select @@ROWCOUNT as Total_Parts_Value

`Output Obtained =1701102`

Only **91.901372%** of records satisfy above Result

    Select * 
    From Amount_Fields_Table
    Where Cast(Cus_Par_Amount as int) +Cast(Inter_Parts_Amount as int) +Cast(Warr_Parts_Amount as int)=Cast(Parts_Amount as int)

    Select @@ROWCOUNT as Total_Parts_Value


`Output Obtained =1769887`

Which is **95.281%** of the Total Records.Though this Result is better than the previous Result,But sill it is not statistically close enough.

    Select Distinct(Dealer Id) 
    From Amount_Fields_Table
    Where (Cast(Cut_Par_Amount as int)+Cast(Inter_Parts_Amount as int)+Cast(Warr_Parts_Amount as int))!=Cast(Parts_Amount as int)

`Output Obtained =93`

Hence almost **96.875%** of the dealers contain data, which does not satisfy above result

Hence above Hypothesis that Parts Amount is split into Customer,Warranty and Internal Component is false

#####5.<a name="RoTotal"></a>*Hypothesis to be proven is Ro_Total Field is Split in Customer_Amount,Customer_Parts,Customer_Misc*

*Validation*

    Select * 
    From Amount_Fields_Table
    Where Ro_Total=0 and (Cast(Cus_Lab_Amount as Int)+Cast(Cut_Par_Amount as Int)+Cast(Cust_Mis_Amount as Int) )=0	

    Select @@ROWCOUNT as Total_Results_Obtained

    Select * from Amount_Fields_Table where Ro_Total=0
    Select @@ROWCOUNT as Values_Present

`Total_Results_Obtained=838750`

`Values_Present=8389375`

Since The Above Result proves that almost **99.9255 %** records satisfy above condition,Hence Above Hypothesis is True.



#####6.<a name="CusNameType"></a> *Hypothesis to be proven is Customer_Name_Type Column contains unique value for every Customer*

Validating Hypothesis
    
    Select 
        Customer_Full_Name,Customer_First_Name,Customer_Last_Name,Email_Address 
        From Dummy_Table
        Where Customer_Name_Type='2'

    Intersect

    Select 
        Customer_Full_Name,Customer_First_Name,Customer_Last_Name,Email_Address 
        From Dummy_Table
        Where Customer_Name_Type='1'

After analysing above output,it was found that there were customers who had both the values of 1 and 2 in Customer_Name_Type.Hence above hypothesis is false.

#####7.<a name="CusNumDeal"></a>*Hypothesis to be proven is dealer assigns unique Customer_Num_Dealer to every Customer* 

Validating Hypothesis

    Select 
        Customer_Num_Dealer,Customer_Full_Name,Dealer_Id,Ro_Number
        From Dummy_Table
        Group By Customer_Num_Dealer,Customer_Full_Name,Dealer_Id,Ro_Number
        Order By Customer_Full_Name,Dealer_Id,Ro_Number

After analysing output,it was found that same customer was assigned different Customer_Num_Dealer by the same dealer for different Ro_Number.Hence above hypothesis is false

#####8.<a name="RawOpCode"></a>*Hypothesis to be proven is Raw_Operation_Code is mapped to Op_Code*

Validating Hypothesis
    
    Select 
        Raw_Dealer_Operation_Code,Op_Codes,Dealer_Id,Parts_Numbers
        From Dummy_Table
        Group By Raw_Dealer_Operation_Code,Op_Codes,Dealer_Id,Parts_Numbers
        Order By Raw_Dealer_Operation_Code,Dealer_Id

After obtaining following output
```
35CHZ12	40	27081	CH4806013-AA
35CHZ13	40	27081	CH5174313-AA
```
It was found that dealer with same Op_code, have different Raw_Dealer_Operation_Code because of change in part number



####8. **Various Hypothesis related to Customer,Warranty And Internal Data Columns**

#####8.1.<a name="CusLabAmo"></a>*Hypothesis to be proven is that Customer_Labour_Amount represents the Customer fraction of Labour Amount from Total Labour Amount*

    Select COUNT(*) as Records_Recieved
    From Amount_Fields_Table
    Where Cus_Lab_Amount=Labour_Amount-Warr_Labou_Amount-Inter_Labour_Amount

`Records_Recieved =1652749`

`Total Records Present =1857537`

Thus it represents only **88.975%** of the total records present in data.Amount of Data  which does not satisfy this condition cannot be ignored,hence above hypothesis is false

#####8.2.<a name="CusParAmo"></a>*Hypothesis to be proven is that Customer_Parts_Amount represents the Customer fraction of Parts Amount from Total Parts Amount*

    Select COUNT(*) as Records_Recieved
    From Amount_Fields_Table
    Where Cut_Par_Amount=Parts_Amount-Warr_Parts_Amount-Inter_Parts_Amount

`Records_Recieved =1703104`

`Total Records Present =1857537`

Thus it represents only **91.68** of the total records present in data.Amount of Data  which does not satisfy this condition cannot be ignored,hence above hypothesis is false

#####8.3.<a name="WarrParAmo"></a>*Hypothesis to be proven is that Warranty_Parts_Amount represents the Warranty fraction of Parts Amount from Total Parts Amount*

    Select COUNT(*) as Records_Recieved
    From Amount_Fields_Table
    Where Warr_Parts_Amount=Parts_Amount-Cut_Par_Amount-Inter_Parts_Amount

`Records_Recieved =1702812`

`Total Records Present =1857537`

Thus it represents only **91.67** of the total records present in data.Amount of Data  which does not satisfy this condition cannot be ignored,hence above hypothesis is false

#####8.4.<a name="WarrLabAmo"></a>*Hypothesis to be proven is that Warranty_Labour_Amount represents the Warranty fraction of Labour Amount from Total Labour Amount*

    Select COUNT(*) as Records_Recieved
    From Amount_Fields_Table
    Where Warr_Labou_Amount=Labour_Amount-Cus_Lab_Amount-Inter_Labour_Amount

`Records_Recieved =1647651`

`Total Records Present =1857537`

Thus it represents only **88.700** of the total records present in data.Amount of Data  which does not satisfy this condition cannot be ignored,hence above hypothesis is false

#####8.5.<a name="IntLabAmo"></a>*Hypothesis to be proven is that Internal_Lab_Amount represents the Internal fraction of Labour Amount from Total Labour Amount*

    Select COUNT(*) as Records_Recieved
    From Amount_Fields_Table
    Where Inter_Labour_Amount=Labour_Amount-Cus_Lab_Amount-Warr_Labou_Amount

`Records_Recieved =1646702`

`Total Records Present =1857537`

Thus it represents only **88.649** of the total records present in data.Amount of Data  which does not satisfy this condition cannot be ignored,hence above hypothesis is false

#####8.6.<a name="IntParAmo"></a>*Hypothesis to be proven is that Internal__Amount represents the Internal fraction of Parts Amount from Total Parts Amount*

    Select COUNT(*) as Records_Recieved
    From Amount_Fields_Table
    Where Inter_Parts_Amount=Parts_Amount-Cut_Par_Amount-Warr_Parts_Amount

`Records_Recieved =1702497`

`Total Records Present =1857537`

Thus it represents only **91.653** of the total records present in data.Amount of Data  which does not satisfy this condition cannot be ignored,hence above hypothesis is false

#####9. <a name="Description"></a> *Hypothesis to be proved is that Description_2 contains additional information*

*Validating Hypothesis*

**Requirement**

Function which would split the column having delimeter

We will create two tables,one for holding Description_1 and other for holding Description_2.Along with that ,both the tables will share common column of Dealer_Id.


    Insert Into Des1 
        Select  Case When ISNUMERIC(t1.Dealer_Id)=1 THEN CAST(t1.Dealer_Id as Int)ELSE NULL END,i.items
        From Dummy_Table t1
        Outer Apply dbo.split(t1.Description_1, '^')i  order by Dealer_Id

Inserting values of Description_2 in second table
    
    Insert Into Des2 
        Select  Case When ISNUMERIC(t1.Dealer_Id)=1 THEN CAST(t1.Dealer_Id as Int)ELSE NULL END,i.items
        From Dummy_Table t1
    Outer Apply dbo.split(t1.Description_2, '^')i  order by Dealer_Id
   
Finding out rows present in one table but not in other
 
    Select Dealer_Id,Description_First 
    From Des2
    Where Not Exists(
                    Select Dealer_Id,Description_First 
                    From Des1
                    Where Des1.Dealer_Id=Des1.Dealer_Id and Des1.Description_First=Des2.Description_First)

###Different Criteria For Calculating Top Dealer

1. One of the criteria For calculating top Dealer could be by categorizing dealers by
  the `Count of Technicians` they possess.This criteria points in the direction of ability to
  handle various operations

2. Second criteria could be by calculating `Labour Time`,for every dealer, for some
  common operation.This could help in categorizing dealer on the basis of hiring/
  possession of efficient dealers

3. Third criteria could be by calculating Total Revenue ,that is sum of `Labour_Amount
   and Parts_Amount`.It divides dealers on the basis of Earnship

4. Fourth criteria could be by finding out `Total Expenditure` By Every Dealer.

5. Fifth criteria could be by calculating `Number Of Distinct Vehicles` visiting each Dealer.This criteria could point in the direction of Reliability of Every Dealer.


###SQL QUERIES FOR DIFFERENT CRITERIA

#####*Query To Fetch Number Of Technicians*

        Create Table #NumberTech
          (
          Dealer_Id INT,
          No_Of_Tech INT
          )

        Insert Into #NumberTech 
          Select  Case When ISNUMERIC(t1.Dealer_Id)=1 THEN CAST(t1.Dealer_Id as Int)ELSE NULL END,
          count(distinct i.items)
          From Dummy Table t1
          Outer Apply dbo.split(t1.Op_Codes, '^')i  group by Dealer_Id order by Count(distinct i.items)
  
        Select * 
        From #NumberTech
        
*Result Analysis*

Dealer Id which is obtained from above query is **21291**.Various factors which might have contributed to this are discussed below

        
Total Records Present For Dealer

        Select COUNT(*) as Total_Records
        From DS4
        Where Dealer_Id='21291'

`Output obtained =29270`

Finding out the city from which maximum repair orders are generated for given dealer

      Select State1,Count(*) as Number_of_Customers,Customer_Full_Name,VIN,Zip 
      From DS4 
      Where Dealer_Id='21291' 
      Group By State1,Customer_Full_Name,VIN,Zip 
      Order By Count(*) desc

On Analysing data it can be clearly seen that Most of the customers are from **New York**.Since New York is one of the densily popluated city of the world so in order to cater the demand,dealer may have to employe more number of technician.

Finding out the different segments of car which are catered

    Select Count(*) as Number_of_Customer,Model_Year,Make_Name,Model_Name
    From DS4 
    Where Dealer_Id='21291' 
    Group By Model_Year,Make_Name,Model_Name
    Order By Count(*) desc

`Total Records=1010`

    Select Count(*) as Number_of_Customer,Model_Year,Make_Name,Model_Name
    From DS4 
    Group by Model_Year,Make_Name,Model_Name
    Order by Count(*) desc

`Total Different Cars Present=6392`

On analysing above data,it can be clearly seen that,this dealer caters to about **15.80%** of the total different type of cars which are present on street.

Graph of Top 5 Dealer based on Number of Technicians is present <>

#####*Query To Find Labour Time For Common Occuring OpCode*
**Checking If Same Op_Codes Exist For Every Code In Order To Calculate Laboue_Time** 

    Create Table #SecondTemp
      (
      Dealer_Id INT,
      Op_Codes VARCHAR(8000)
      )

      Select 
        Dealer_Id,Op_Codes From Dummy Table 
        Group by Op_Codes,Dealer_Id 
        Order by Dealer_Id
    
    
      Insert Into #SecondTemp 
        Select Case When ISNUMERIC(Dealer_id)=1 THEN CAST(Dealer_Id as Int)ELSE NULL END , Op_Codes 
        From Dummy Table 
        Group by Op_Codes,Dealer_Id 
        Order by Dealer_Id

      Select Op_Codes,COUNT(*) 
      From #SecondTemp 
      Group by Op_Codes Having COUNT(*)>91

#####*Query For Finding Labour_Time For The Deduced Op_Code*

Creating Table For Op_Code=40 Present In All The Dealer_Id
       
    Create Table #LabourTime
    (
    Dealer_Id INT,
    Labour_Time Float
    )
    Insert Into #LabourTime Select distinct Dealer_Id,Labour_Time From DS3 where Op_Codes='40'

    Insert into #LabourTime 
      Select  Dealer_Id,SUM(CASE WHEN ISNUMERIC(Labour_Time)=1 THEN CONVERT(FLOAt,Labour_Time)ELSE NULL END) 
      From Dummt Table 
      Where Op_Codes='40' 
      Group by Dealer_Id

Delete From #LabourTime

    Select * from #LabourTime

#####*Query For Determining Number Of Distinct Vehicles*

Creating Table Which Stores The Count Of Each VIN in Every Dealer

    Create Table #ValCal
      (
      Dealer_Id INT,
      VIN VARCHAR(8000),
      Total_Rows INT
      )

--Drop Table #ValCal

    Insert Into #ValCal 
      Select  Case When ISNUMERIC(Dealer_id)=1 THEN CAST(Dealer_Id as Int)ELSE NULL END,VIN,COUNT(*) as Total_Rows 
      From Dummy Table 
      Group By VIN,Dealer_Id  
      Order By Dealer_Id

--Creating Table For Storing Dealer Id's Along With their Number Of Distinct Vehicles

    Create Table #DisVeh
      (
      Dealer_Id INT,
      Total_Distinct_Vehicle INT
      )
 
    Insert Into #DisVeh Select Dealer_Id,COUNT(*) from #ValCal  group by Dealer_Id

#####*Query To Fetch Revenue Generated For Every Dealer*

--Creating Table to store Revenue generated by every dealer

    Create Table #Revenue
      (
      Dealer_Id INT,
      Labour_Amount Float,
      Parts_Amount Float
      )

    Insert Into #Revenue 
      Select Case When ISNUMERIC(Dealer_id)=1 THEN CAST(Dealer_Id as Int)ELSE NULL END,SUM(CASE WHEN ISNUMERIC(Labour_Amount)=1 THEN CONVERT(FLOAt,Labour_Amount)ELSE NULL END),SUM(CASE WHEN ISNUMERIC(Parts_Amount)=1 THEN CONVERT(FLOAT,Parts_Amount) ELSE NULL END)
      From Dummy Table 
      Group By Dealer_Id  


    Create Table #Rev_Final
      (
      Dealer_Id INT,
      Total_Revenu Float
      )

    Insert Into #Rev_Final 
      Select Dealer_Id,Labour_Amount +Parts_Amount  
      From #Revenue

*Result Analysis*

Dealer Id which is obtained from above query is **9774**.Various factors which might have contributed to this are discussed below

Finding out total records present for given dealer
    
    Select COUNT(*) 
    From DS4
    Where Dealer_Id='9774'

`Output Obtained =93388`

On Analysing this output it clear that this dealer has the **2nd** highest number of records,which is one of the major contributing factor for revenue.

Finding out different states from which orders are generated for given dealer

    Select State1,Count(*) 
    From DS4
    Where Dealer_Id='9774'
    Group by State1

`Output Obtained =50`

    Select State1 
    From DS4
    Group by State1

`Output Obtained =88`

It is clearly evident that, this dealer caters to customer of about **56.18%** of states

Finding out the type of cars which are catered by given dealer

    Select Model_Year,Count(*)
    From DS4
    Where Dealer_Id='9774'
    Group By Model_Year
    Order By Count(*) Desc 
```
Output obtained

2010	13085
2011	12153
2009	10077
2008	9928
2006	8659
2007	7710
2005	6837
2004	5475
2003	4322
2012	3441
2002	3320
2001	2705
2000	1779
1999	1187
1998	682
1997	566
1996	428
1995	341
1994	148
1992	130
1993	107
1991	92
1990	53
1988	37
1987	30
1986	25
1989	23
1984	13
1976	8
1985	7
1983	3
1978	3
1967	3
1973	2
2013	2
1971	1
1980	1
1972	1
1975	1
1982	1
1981	1
1974	1
```

    Select Distinct(Model_Year)
    From DS4
    Order By Model_Year

`Output Obtained =74`


On Analysing above results, two Conclusions can be drawn.

First would be that this dealer has request from 56.76% different available car on the basis of Model_Year.

But the main reason why this dealer might be earning large amount of revenue can come by observing aobe result,which clearly shows the car of model year **2010** has the maximum records.This number is significant in that aspect because as time passes there is more wear and tear associated happening of car.So  dealer catering car of Model year 2010 would more likely to generate more revenue from the one catering car of Model Year 2013 or 2014.

Top 5 Dealers can <>



#####*Query To Fetch Expenditure For Every Dealer*

--Splitting Labour_Op Per Dealer

    Create Table #Labour_Per_Op
      (Dealer_Id Int,
      Labour_Per_Op Float
      )


    Insert Into #Labour_Per_Op  
      Select Case When ISNUMERIC(Dealer_id)=1 THEN CAST(Dealer_Id as Int)ELSE NULL END,SUM(CASE WHEN ISNUMERIC(i.items)=1 THEN CONVERT(FLOAt,i.items)ELSE NULL END)
      From Dummy Table t1
      outer apply dbo.split(t1.Labor_Per_Op, '^')i  
      Group By Dealer_Id
      

--Splitting Parts_Op Per Dealer

    Create Table #Parts_Per_Op
      (Dealer_Id Int,
      Parts_Per_Op Float
      )
    Insert Into #Parts_Per_Op  
      Select Case When ISNUMERIC(Dealer_id)=1 THEN CAST(Dealer_Id as Int)ELSE NULL END,SUM(CASE WHEN ISNUMERIC(i.items)=1 THEN CONVERT(FLOAt,i.items)ELSE NULL END)
      From Dummy Table t1
      outer apply dbo.split(t1.Parts_Per_Op, '^')i  
      Group By Dealer_Id 

--Creating Table Which Would Contain The Sum Of  Lavour_Per_Op And Parts_Per_Op

    Create Table #Exp_Final
      (
      Dealer_Id Int,
      Total_Expend Float
      )

    Insert Into  #Exp_Final(Dealer_Id) 
      Select Dealer_Id from #Labour_Per_Op 

--Joining Above Created Tables To Fill Final Table

    Update #Exp_Final 
    Set Total_Expend=#Labour_Per_Op.Labour_Per_Op+#Parts_Per_Op.Parts_Per_Op 
    From #Labour_Per_Op,#Parts_Per_Op,#Exp_Final 
    Where #Exp_Final.Dealer_Id=#Labour_Per_Op.Dealer_Id and #Exp_Final.Dealer_Id=#Parts_Per_Op.Dealer_Id






