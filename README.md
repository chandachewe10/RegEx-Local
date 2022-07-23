## About ReGex Local

This is PHP RegEx which can assist developers specifically in Zambia to validate users where those users are using local content variables such as local names, Local National ID's, Local Mobile Numbers etc. The RegEx can be extended and applied to other foreign data as well such as foreign names, passwords etc. PHP RegEx is used here however it can easily be converted to other RegExes as well such as Java, JavaScript etc.

1. ## Validating Zambia Local Mobile Phone Numbers

Zambia local mobile phone numbers consists of 10 digits and starts with either 09 or 07. The RegEx below works perfectly.

`/^(09|07)[5|6|7][0-9]{7}$/`

### Meaning <br>
a. `/` - Start a regex <br>
b. `^(09|07)` - The phone number should start with either 09 or 07 <br>
c. `[5|6|7]` - The number then should be followed with either 5 or 6 or 7 <br>
d. `[0-9]{7}$` - The number should end with 7 digits with each digit between 0 and 9. <br>
e. `/` - Close a regex <br>

### Use Case - PHP
`if (preg_match('/^(09|07)[5|6|7][0-9]{7}$/'),$phone){` <br> 
    //Phone number matches with either Mtn Zambia/Airtel Zambia/Zamtel <br>
`}` <br>
`else{` <br>
   ` echo 'Your phone number is invalid. Your phone must begin with either 096 0r 097 or 095'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL
`'phone' => ['regex:/^(09|07)[5|6|7][0-9]{7}$/'],` <br>


Note: If you want to validate the mobile phone number to international format where your users have to start with 26 then your regex will be <br>
- `/^(2609|2607)[5|6|7][0-9]{7}$/`




<br><br><br><br>


2. ## Validating Zambia National Identity Number(s) (NRC) <br>

Zambia National Identity Number consists of 9 digits and two foward slashes in this format `******/**/*`. This regEx seems to be working. <br>
`/^(\d{6})\/\d{2}\/\d{1}$/` <br>

### Meaning <br>
a. `/` - Start a regex <br>
b. `^` - The NRC should start as....  <br>
c. `\d{6}` - The NRC should start with 6 digits. Please note that this is equivalant to `[0-9]{6}`  <br>
d. `\` - Escape character to start a foward slash <br>
e. `/` - Foward slash. <br>
f. `\d{2}` - The NRC should contain two digits after the first foward slash. Please note that this is equivalant to `[0-9]{2}`  <br> 
g. `\` - Escape character to start another foward slash <br>
h. `/` - Foward slash. <br>
i. `\d{1}$` - The NRC should end with 1 digit after the last foward slash. Please note that this is equivalant to `[0-9]{1}`  <br>
j. `/` - End a regex <br>

### Use Case - PHP <br>
`if (preg_match('/^(\d{6})\/\d{2}\/\d{1}$/'),$nrc){` <br>
    //NRC Matches with Zambian NRC Standard <br>
`}`
`else{` <br>
   ` echo 'Your NRC is invalid. Your NRC must be in this format ******/**/*'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL <br>
`'nrc' => ['regex:/^(\d{6})\/\d{2}\/\d{1}$/'],` <br>



<br><br><br><br>





3. ## Validating Local Common Names <br>

Common Names here refers to simple names without special characters, names like `chanda` `chewe` etc. <br>

### A. Validating first name only <br>
-There are some cases where you can divide the input form into 3 separate fields and you would want users to enter their first name only. This regex works fine. <br>
`/^[a-zA-Z]{2,50}$/` <br>

### Meaning <br>
a. `/` - Start a regex <br>
b. `^[a-zA-Z]` - The first name should start with with either small letter or capital letter   <br>
c. `{2,50}$` - The first name should be between two to fifty characters long. <br>
d. `/` - End regex. <br>
 

### Use Case - PHP <br>
`if (preg_match('/^[a-zA-Z]{2,50}$/'),$first_name){` <br>
    //Matches names like Chanda, Chewe, musonda, Mwamba etc <br>
`}` <br>
`else{` <br>
   ` echo 'Your name is invalid. Ensure your first name does not contain spaces'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL <br>
`'first_name' => ['regex:/^[a-zA-Z]{2,50}$/'],` <br>





### B. Validating first name and last name only <br>
-There are some cases where you want the user to enter the first name and last name only. This regex will help. <br>
`/^([a-zA-Z]){2,50}\s([a-zA-Z]){2,50}$/` <br>

### Meaning <br>
a. `/` - Start a regex <br>
b. `^([a-zA-Z])` - The first name should start with with either small letter or capital letter   <br>
c. `{2,50}` - The first name should be between two to fifty characters long. <br>
d. `\s` - Allow the user to leave one white space. <br>
e. `[a-zA-Z]` - The surname should start with with either small letter or capital letter. <br>
f. `{2,50}$` - The surname should end between two to fifty characters long. <br>
g. `/` - Close a regex <br>
 

### Use Case - PHP <br>
`if (preg_match('/([a-zA-Z]){2,50}\s([a-zA-Z]){2,50}$/'),$full_name){` <br>
    //Matches names like Chanda Chewe, musonda Mwamba, etc <br>
`}` <br>
`else{` <br>
   ` echo 'Your Full Name is invalid'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL <br>
`'first_name' => ['regex:/([a-zA-Z]){2,50}\s([a-zA-Z]){2,50}$/'],` <br>




### C. Validating First name, Last name and Middlename Sometimes <br>
-There are some cases where you want the user to enter the full name with Middlename in between sometimes. This regex seems to work. <br>
`/^([a-zA-Z]){2,256}\s(([a-zA-Z]){2,256}\s)?([a-zA-Z]){2,50}$/` <br>

### Meaning <br>
a. `/` - Start a regex <br>
b. `[a-zA-Z]` - The first name should start with with either small letter or capital letter   <br>
c. `{2,256}` - The first name should be between 2 to 256 characters long . <br>
d. `(([a-zA-Z]){2,256}\s)?` - The question mark at the end implies that there is a possibility of having characters between 2 and 256 here and a white space. <br>
e. `[a-zA-Z]` - The surname should start with with either small letter or capital letter. <br>
f. `{2,50}$` - The surname should end between two to fifty characters long. <br>
g. `/` - Close a regex <br>
 

### Use Case - PHP <br>
`if (preg_match('/^([a-zA-Z]){2,256}\s(([a-zA-Z]){1,256}\s)?([a-zA-Z]){2,50}$/'),$full_names){` <br>
    //Matches names like Chanda henschel Chewe, musonda kalunga Mwamba etc <br>
`}` <br>
`else{` <br>
   ` echo 'Your Full Name is invalid'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL <br>
`'first_name' => ['regex:/^([a-zA-Z]){2,256}\s(([a-zA-Z]){1,256}\s)?([a-zA-Z]){2,50}$/'],` <br>




<br><br><br><br>





4. ## Password Validations <br>

Common password Validations. <br>

### A. 8 Atleast Characters Long <br>
-There are some cases where you want to implement a password of length 8 characters or more and ends there. This regex can help <br>
`/^(\d{8,})$/` <br>

### Meaning <br>
a. `/` - Start a regex <br>
b. `^()` - The password should contain...  <br> 
c. `\d{8,}$` - More than 8 digits without letters and special characaters. <br>
d. `/` - End regex. <br>
 

### Use Case - PHP <br>
`if (preg_match('/^(\d{8,})$/'),$password){` <br>
    //Matches weak passwords 12345678, 277477388292092, etc <br>
`}` <br>
`else{` <br>
   ` echo 'Your password must contain more than 8 digits'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL <br>
`'password' => ['regex:/^(\d{8,})$/'],` <br>





### B. 8 Atleast Characters Long, & Contains Atleast One Uppercase, One Lower Uppercase, A Number, & A Special Character  <br>
- This is the recommended way of passwords implementations. The regex below might help  <br>
`/(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[_@$!%*#?&]).{8,}$/` <br>

### Meaning <br>
a. `/` - Start a regex <br>
b. `?=.*` - should contain atleast... <br>
c. `\d` - Must have atleast one digit. This is equivalent to `[0-9]`; <br>
d. `?=.*` - should contain atleast... <br>
e. `[a-z]` - Must have atleast a lowercase character. <br>
f. `?=.*` - should contain atleast... <br>
g. `[a-z]` - Must have atleast an uppercase character. <br>
h. `?=.*` - should contain atleast... <br>
i. `_@$!%*#?&` - Should contain a special character <br>
j. `.` - It can contain any multiple character <br>
k. `{8,}$` - All characters must be greater than or equal to 8 at end <br>
l. `/` - End regex. <br>
 

### Use Case - PHP <br>
`if (preg_match('/(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[_@$!%*#?&]).{8,}$/'),$password){` <br>
    //Matches strong passwords <br>
`}` <br>
`else{` <br>
   ` echo 'Your password must be 8 characters long and must contain an uppercase, lowecase, number and a special character'; ` <br>
`}` <br>


### Use Case - PHP LARAVEL <br>
`'password' => ['regex:/(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[_@$!%*#?&]).{8,}$/'],` <br>



## Contributing <br>

Feel free to make a Pull Request, As long as you are not correcting a spelling. Meaningful PR involves fixing errors and adding more RegExes.  <br>


## Errors <br>

If you discover that a certain ReGex is not working and you are not familiar with ReGex, please raise an Issue on this repo or send an e-mail to Chanda Chewe via [chewec03@gmail.com](mailto:chewec03@gmail.com). All vulnerabilities will be promptly addressed. <br>

## License <br>

This repo is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT). <br>
