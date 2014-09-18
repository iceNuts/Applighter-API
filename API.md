Applighter API
================

#### 学校信息api
  - base URL: /webapp/school
    
  - GET: 
            /webapp/school/o/object_id

           Get One School Information in Json

           /webapp/school/a/schoolrank 

           schoolrank == 1 前50
           schoolrank == 2 50到100
           schoolrank == 3 100到150



#### 上传文件api


  - POST URL: /webapp/ajax/upload/file

  - url后面跟参数为userid
        -- example: /webapp/ajax/upload/file/5403cbafc030e25f861b482f

  - post本身不带参数

  - Available file types:

    - file_types = ['docx', 'pdf', 'doc', 'docm', 'dotx', 'dotm', 'txt', 'jpeg', 'png', 'jpg','xls','xlsx','ppt','pptx']
  
 


#### Session字段说明

  - Schema:

        COOKIE {
            userid: user_id
            token: token
        }



#### User用户api

  
  - register 

    - URL : /webapp/register

    - POST :

          Post email, password and user_type to register as a user.

      POST Json Example:

          {
            "email" : "billzeng808@gmail.com",
            "password" : "123",
            "user_type" : "1"/"2"/"4" 1 is counselor; 2 is student; 4 is parent
          }

  - login (30 days expire)

    - URL : /webapp/login

    - POST :

          Post email and password to login, server would return an url. Redirect this url to right place.

      POST Json Example:

          {
            "email" : "billzeng808@gmail.com",
            "password" : "123"
            "user_type" : "0"/"1"/"2"/"4" 0 is CounselorAdmin; 1 is Counselor; 2 is Student; 4 is Parent
          }

      User status code:

          2001  active student but detailed information is not completed -> detailed page
          2002  inactive student and general information is not completed -> basic info page
          2003  inactive student and general information is completed -> school map view page

          3001  active student with everything done -> student dashboard page
          3002  archived student -> student summary page

          4001  Parent logged in
          4002  Counselor logged in
          4003  Counselor Admin logged in

      Return example:
          
          {
              "result" : "2003",
              "userid" : ".."
          }


  - check register email valid

    - URL : /webapp/register/check

    - POST :

        Post email to check if it has been registered.

      POST Json Example:

          {
            "email" : "billzeng808@gmail.com"
          }   

  - validate user password

    - URL : /webapp/validatepassword 

    - POST : 

        Post user's old password to validate.

            { 
              'password' : old password
            }

            Then use user put method to update new password

  - User 

      Return 200 OK or 500 Error

    - PUT

        - URL : /webapp/user

          Put Json to update user infomation.

              Availabe keys:

              name

              title
          
              avatar : string
          
              contact_list : Dict
          
              user_name
          
              user_passwd
          
              gender : 0 girl 1 boy
          
              school
          
              year
          
              target : undergraduate? graduate? highschool?
          
              rank_in_school 
          
              gpa_in_school : float
          
              score_list : Dict
          
              major_interest : string
          
              general_info : String

              example :

              {
                 "taskgroup_list":[

                 ],
                 "user_type":2,
                 "rank_in_school":"top20",
                 "year":"高三",
                 "general_info":"我去。。这都是假的吧",
                 "title":"学生",
                 "active_status":0,
                 "score_list":{
                    "SAT":{
                       "overall":"1680",
                       "math":"620"
                    }
                 },
                 "schedule_event_list":[

                 ],
                 "user_name":"14ed2b0d82fe94312618ea8183127f6d",
                 "counselor_list":[

                 ],
                 "gpa_in_school":3.3,
                 "contact_list":{
                    "phone":"333-222-111",
                    "email":"liuyuxiao123@gmail.com",
                    "address":"窝里蹲"
                 },
                 "target":"undergraduate",
                 "news_feed_list":[

                 ],
                 "school":"Beihang U",
                 "name":"刘总",
                 "gender":0,
                 "avatar":"http://applighter-data-node-a.oss-cn-hangzhou.aliyuncs.com/AWS/2588f953575885b888dbbbfdd48410aa-1406019285.65.jpg",
                 "user_passwd":"202cb962ac59075b964b07152d234b70",
                 "_cls":"User.Student",
                 "major_interest":"约炮"
              }

    - GET

        - URL : /webapp/user/o/obj_id


    - DELETE

        - URL : /webapp/user/o/obj_id

   

    - USER ACTIVATION (Gmail Enterprise As Mail Server)

        Return 200 or 500 error

        - URL : /webapp/student/activate

        - POST :

                {
                  "userids":
                  [
                    id_0,
                    id_1,
                    ...
                  ]
                }

            Server will send emails to those users with a activation code.

        - GET :

            User click on the activation url. Frontend should check if the cookie holds userid and token(logged in?). If not logged in, frontend should redirect user to login view, afterwards, continue redirecting to activation url.


    - 获取学生顾问列表api
        - URL : /webapp/usercounselor/o/userid
        - GET 方法 URL中带userid参数

    - 获取学生近期任务列表api
        - URL : /webapp/user/recenttask/o/userid
        - GET 方法 URL中带userid参数


  - Counselor

    - POST 

        Create a new counselor

        - URL : /webapp/admin/counselor

          Json example:

              {
                "name":"LI",
                "avatar":"", 
                "email":"oops",
                "password":"123"
              }

              All fields above are required

  - Student

    - LINK A COUNSELOR

      Link a counselor when register (At least one counselor)

      - URL : /webapp/student/linkcounselor

          Json example:

              {
                "email":"oops"
              }

          Put Counselor user name(email). Student should logged in.


#### TaskGroup学校列表

 
  - GET :

      - URL : /webapp/taskgroup/o/obj_id

            Get one taskgroup by obj_id

      - URL : /webapp/taskgroup/u/userid

            Get all taskgroups by userid

  - PUT :

      - URL : /webapp/taskgroup

        - Counselor update student taskgroup info

                {
                    "taskgroup": taskgroup id,
                    "alias": TG name, 
                    "description": TG description,
                    "userid": TG task owner id,
                }

  - DELETE :

      - URL : /webapp/taskgroup/o/obj_id

        - Counselor deletes a taskgroup by id

#### Task学生任务

  - POST :

      - URL : /webapp/task

        - Create a new Task

                {
                   "alias": Task name,
                   "owner" : owner id,
                   "description" : Task description,
                   "taskgroup": TG id,
                   "associate_owners": [id, id_1...],
                   "deadline": "2014-03-24 03:24"
                }

            create a Task for a TaskGroup

  - GET :

      - URL : /webapp/task/o/task id

            Get one Task by Task id

      - URL : /webapp/task/u/taskgroup id

            Get all Tasks by TG id

  - PUT :

      - URL : /webapp/task

        - Counselor update student taskgroup info

                {
                    "task": task id
                    "alias": task name,
                    "description": TG description,
                    "associate_owners": everybody who is involved, id,
                    "deadline": "UTC timestamp",
                }

  - DELETE :

      - URL : /webapp/task/o/task id

        - Counselor deletes a taskgroup by id

#### Comment

  - POST :

      - URL : /webapp/op/comment

        - Create a new Comment

                {
                   "owner": owner object id, Post/Task
                   "comment_type": 0 post / 1 task / 2 award / 3 doings / 4 appfile
                   "content": what you say
                }

            create a Comment for a Task

  - GET :

      - URL : /webapp/op/comment?timestamp=(float)&limit=(int)&tid=(id)&type=(type)

            Get a list of comments of a task/post before timestamp limited by a number

            Example:

                /webapp/task/comment/?timestamp=1405659283&limit=1&tid=53c77ccad4901831badcb98d

#### Activity

  - POST :

      - URL : /webapp/user/activity

        - Get a list of activity

              activity_types = {
                      'post' :        0,     
                      'comment' :     1,      
                      'appfile' :     2,      
                      'task' :        3,      
                      'deadline' :    4,     
                      'taskgroup' :   8,      
                      'award':        9,
                      'doings':       10,
                      'counselor' :   101,     
                      'school' :      102,      
                              }


                Based on type:

                function type : 0, get activity by limit

                {
                   "func_type" : "0"
                   "limit": an int number,
                   "timestamp": timestamp, utc float
                   "revert": 
                    1 True search the past from timestamp
                    (t1 <= t2 <= t3 <= ... <= timestamp), 
                    0 False search the future from timestamp
                    (timestamp <= t1 <= t2 <= t3 ... <= tn)
                   "type": int activity type
                }

                function type : 1, get activity by timestamp

                {
                   "func_type" : "1"
                   "from_timestamp": timestamp, utc float
                   "end_timestamp": timestamp, utc float
                   "type": int activity type
                }

                from_timestamp < end_timestamp


                API Based on priority:

                high priority is on main page, low pirority is in inbox

                function type : 2, get activity by limit

                {
                   "func_type" : "2"
                   "limit": an int number,
                   "timestamp": timestamp, utc float
                   "revert": 
                    1 True search the past from timestamp
                    (t1 <= t2 <= t3 <= ... <= timestamp), 
                    0 False search the future from timestamp
                    (timestamp <= t1 <= t2 <= t3 ... <= tn)
                   "priority": "1" 0 low / 1 high
                }

                function type : 3, get activity by timestamp

                {
                   "func_type" : "3"
                   "from_timestamp": timestamp, utc float
                   "end_timestamp": timestamp, utc float
                   "priority": "0" 0 low / 1 high
                }

                Return JSON example:

                {
                   "result": [
                      {
                          "_id": "53cf7dafd4901859f175cdca", 
                          "user_id": "53c4e5bed49018d78cbb42ea", 
                          "read": 0,
                          "activity_type": 1, 
                          "description": "\u5218\u603b\u5728OO TASK\u6dfb\u52a0\u4e86\u4e00\u6761\u8bc4\u8bba:\"example2\"", 
                          "short_description" : "",
                          "update_time": "2014-07-23T09:17:35.995", 
                          "link": "53c77d22d4901831dd362b8d", 
                          "dictionary": {}
                      }, 
                      {
                          "_id": "53cf7c68d49018589ae16438", 
                          "user_id": "53c4e5bed49018d78cbb42ea", 
                          "read": 0,
                          "activity_type": 1, 
                          "description": "\u5218\u603b\u5728OO TASK\u6dfb\u52a0\u4e86\u4e00\u6761\u8bc4\u8bba:\"example\"", 
                          "short_description" : "",
                          "update_time": "2014-07-23T09:12:08.077", 
                          "link": "53c77d22d4901831dd362b8d", 
                          "dictionary": {}
                      }
                   ]
                }

  - PUT :

      - URL : /webapp/user/activity

        - Update a list of activities read status to be 'read'

                {
                    "activities" : [a_0, a_1, a_2 ... a_n]
                }

                activity ids

#### Device

  - POST/PUT :

      - URL : /webapp/user/device

        - Register/Update a user's device

                device_type_options = {
                    'iOS' : 0,
                    'Android' : 1
                }

                {
                    "type" : device type,
                    "token" : device push token,
                    "udid" : device udid
                }

#### Alert

  - POST :

      - URL : /webapp/op/alert

        - Create an alert for a task/or something later

                alert_owner_types = {
                  'task' : 0
                }

                {
                    "object_owner_id" : object owner id (for example, task id),
                    "owner_type" : owner type int,
                    "trigger_time" : "2014-05-06 13:55"
                }

  - PUT :

      - URL : /webapp/op/alert

        - Register/Update a user's device

                device_type_options = {
                    'iOS' : 0,
                    'Android' : 1
                }

                {
                    "obj_id" : alert object id,
                    "trigger_time" : "2014-05-06 13:55"
                }

  - GET :

      - URL : /webapp/op/alert/u/obj_owner_id

        - Get a list of alerts by object owner id (for example, task id)

  - DELETE :

      - URL : /webapp/op/alert/u/obj_id

        - Delete alert by alert id

#### Award

  - POST :

      - URL : /webapp/user/award

        - Create an award for user

                {
                    "alias" : award name,
                    "description" : details
                }

  - PUT :

      - URL : /webapp/user/award

        - Update an award 

                {
                    "award" : award obj id
                    "alias" : award name,
                    "description" : details
                }

  - GET :

      - URL : /webapp/user/award/o/obj_id

        - Get an award info by award object id

      - URL : /webapp/user/award

        - Get a list of awards by user id

  - DELETE :

      - URL : /webapp/user/award/o/obj_id

        - Delete an award by award id

#### Doings

  - POST :

      - URL : /webapp/user/doings

        - Create a doings for user

                {
                    "alias" : doings name,
                    "description" : details
                }

  - PUT :

      - URL : /webapp/user/doings

        - Update an doings 

                {
                    "doings" : doings obj id
                    "alias" : doings name,
                    "description" : details
                }

  - GET :

      - URL : /webapp/user/doings/o/obj_id

        - Get an doings info by doings object id

      - URL : /webapp/user/doings

        - Get a list of awards by user id

  - DELETE :

      - URL : /webapp/user/doings/o/obj_id

        - Delete an doings by doings id

#### SchoolChoice

  - POST :

      - URL : /webapp/op/schoolchoice

        - Create a schoolchoice for user

                {
                    "alias" : schoolchoice name,
                    "owner" : owner userid,
                    "school": school object id,
                    "status" : 0 in watchlist / 1 in active list
                }

  - PUT :

      - URL : /webapp/op/schoolchoice

        - Update a schoolchoice 

                {
                    "school" : school obj id
                    "status" : 0 in watchlist / 1 in active list
                }

  - GET :

      - URL : /webapp/op/schoolchoice/o/obj_id

        - Get a school choice info by object id

      - URL : /webapp/op/schoolchoice/u/userid

        - Get a list of school choices by user id

  - DELETE :

      - URL : /webapp/op/schoolchoice/o/obj_id

        - Delete a schoolchoice by objcet id

##### POST

  - POST :

      - URL : /webapp/post

        - Create a new post

                {
                  "alias" : post name,
                  "description" : description,
                  "associate_owner_list" : user id list, involved users
                }

  - PUT :

      - URL : /webapp/post

        - Update a post

                {
                  "post" : post object id,
                  "alias" : post name,
                  "description" : description,
                  "associate_owner_list" : user id list, involved users
                }

  - GET :

      - URL : /webapp/post/o/obj_id

        - Get the post info

      - URL : /webapp/post/u?timestamp=(float)&userid=(int)&limit=(id)&type=(type)

            Get a list of comments of a task/post before timestamp limited by a number

            Example:

                /webapp/task/comment/?timestamp=1405659283&limit=1&tid=53c77ccad4901831badcb98d&type=1

  - DELETE :

      - URL : /webapp/post/o/obj_id




 
  





    
    








