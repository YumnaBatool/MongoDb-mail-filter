MongoDb-mail-filter
======================================

Filters a database of emails by most recent and major senders

CONNECTION STEPS:
1-Download and Install MongoDB 

2-Open Command Prompt as Administration

3-Open the folder with mongodb files by entering this code in shell

  > C:\mongodb\bin        //change folder accordingly
  
4-code to start mongodb

  > mongo
  
5-code to connect to email data base

  > mongo ds039850.mongolab.com:39850/yumna_database -u yumnabatool -p yumnabatool
  
  (above database is the free sandbox at Mongolab contains the emails dummy database)


GETTING LATEST 10 EMAILS:
6-code that looks into emails collection and gets latest 10 emails by date

  >db.myemails.find().sort({"time": 1}).limit(10)
  
  ("myemails" is the dummy database at Mongolab database "yumna_database")
  
GETTING TOP 50 MAJOR SENDERS:
7-code that gets top 50 users who have sent most emails
  >db.myemails.aggregate(
                     [
                        { $group: { _id: "$senderemail", total: { $sum: 1 }  } },
                        { $sort: { total: -1 } },
		                    { $limit : 50 }
                     ],
                     {
                       explain: true
                     }
                   )
