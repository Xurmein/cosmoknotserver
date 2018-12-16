# cosmoknotserver
deployed @ https://cosmoknotserver.herokuapp.com 

## Routes & tokenization
### Exposed Endpoints: 
   No token required.
   
  #### User Table (`user.is_admin===true`) **C**rud
  + register new admin: `${url}/user/register/admin`
    - HTTP method: POST
  + login as admin/user: `${url}/user/login`
    - HTTP method: POST
    - allows login for *all* returning users, no matter admin-status
    
### sessionToken-Protected Endpoints: 
   Routes that use validate-session to check for a 'sessionToken'.  
   Items marked with an '*' are in-progress associations stil being developed.  
   
  #### Content **CRUD** Table
  + create new post (as journalEntry* or readingListItem*): `${url}/myaccount/new_post`
    - HTTP method: POST
  + get *all* user's content posts: `${url}/myaccount/userposts`
    - HTTP method: GET
  + get *one* of user's content posts: `${url}/myaccount/userposts/:id`
    - HTTP method: GET
  + update *selected* personal content post: `${url}/myaccount/userposts/edit/:id`
    - HTTP method: PUT
  
  #### User Table(`user.is_admin === true || user.is_admin !== true`) cr**UD**
  + update personal account info: `${url}/user/update_account/:id`
    - HTTP method: PUT
  + delete personal account: `${url}/user/delete_account/:id`
    - HTTP method: DELETE
    
### adminToken-Protected Endpoints:
   Routes that use validate-admin to check for an 'adminToken'.  
   
  #### User Table(`user.is_admin === true`) **CR**ud
  + create new user: `${url}/user/register/new_user`
    - HTTP method: POST
      - *Only* method to create non-admin users.
  + get *all* users created by admin: `${url}/user/sub-users`
    - HTTP method: GET
  + get *one* user created by admin: `${url}/user/sub-users/:id`
    - HTTP method: GET
  
## Models:
```
{
  user:{
     username:{ 
         type : DataType.STRING,
         allowNull : false,
         unique : true
         },
     password:{
         type : DataType.STRING,
         allowNull : false
         },
     is_admin:{  
         type : DataType.BOOLEAN,
         allowNull : true
         },
     adminID:{
         type : DataType.STRING,
         allowNull : true,
         unique : false,
         validate:{
           isEmail : true
         }
     } 
}
---
{ 
 content:{
   creator:{ 
     type : DataType.STRING, 
     allowNull : false
    },
   label:{
     type : DataType.STRING,
     allowNull : false
     },
   content_text:{
     type : DataType.TEXT,
     allowNull : false
    }
}
```

