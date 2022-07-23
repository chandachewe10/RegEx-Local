## About Filtration

This is PHP RegEx which can assist developers specifically in Zambia to validate users where those users are using local content variables such as local names, Local National ID's, Local Mobile Numbers etc. The RegEx can be extended and applied to other foreign data as well such as foreign names, passwords etc. PHP RegEx is used here however it can easily be converted to other RegExes as well such as Java, JavaScript etc.

1. ## Validating Zambia Local Mobile Phone Numbers

Zambia local mobile phone numbers consists of 10 digits and starts with either 09 or 07. The RegEx below works perfectly.

`/^(09|07)[5|6|7][0-9]{7}$/`

### Meaning
a. `/` - Start a regex
b. `^(09|07)` - The phone number should start with either 09 or 07
c. `[5|6|7]` - The number then should be followed with either 5 or 6 or 7
d. `[0-9]{7}$` - The number should end with 7 digits with each digit between 0 and 9.
e. `/` - Close a regex

### Use Case - PHP
`if (preg_match('/^(09|07)[5|6|7][0-9]{7}$/'),$phone){`
    //Phone number matches with either Mtn Zambia/Airtel Zambia/Zamtel
`}`
`else{`
   ` echo 'Your phone number is invalid. Your phone must begin with either 096 0r 097 or 095'; `
`}`


### Use Case - PHP LARAVEL
`'phone' => ['regex:/^(09|07)[5|6|7][0-9]{7}$/'],`


Note: If you want to validate the mobile phone number to international format where your users have to start with 26 then your regex will be
- `/^(2609|2607)[5|6|7][0-9]{7}$/`



2. ## Validating Zambia National Identity Number(s) (NRC)

Zambia National Identity Number consists of 9 digits and two foward slashes in this format `******/**/*`. This regEx seems to be working.
`/^(\d{6})\/\d{2}\/\d{1}$/`

### Meaning
a. `/` - Start a regex
b. `^` - The NRC should start as.... 
c. `\d{6}` - The NRC should start with 6 digits. Please note that this is equivalant to `[0-9]{6}` 
d. `\` - Escape character to start a foward slash
e. `/` - Foward slash.
f. `\d{2}` - The NRC should contain two digits after the first foward slash. Please note that this is equivalant to `[0-9]{2}`  
g. `\` - Escape character to start another foward slash
h. `/` - Foward slash.
i. `\d{1}$` - The NRC should end with 1 digit after the last foward slash. Please note that this is equivalant to `[0-9]{1}`  
j. `/` - End a regex

### Use Case - PHP
`if (preg_match('/^(\d{6})\/\d{2}\/\d{1}$/'),$nrc){`
    //NRC Matches with Zambian NRC Standard
`}`
`else{`
   ` echo 'Your NRC is invalid. Your NRC must be in this format ******/**/*'; `
`}`


### Use Case - PHP LARAVEL
`'nrc' => ['regex:/^(\d{6})\/\d{2}\/\d{1}$/'],`





3. ## Validating Local Common Names

Common Names here refers to simple names without special characters, names like `chanda` `chewe` etc.

### A. Validating first name only
-There are some cases where you can divide the input form into 3 separate fields and you would want users to enter their first name only. This regex works fine.
`/^[a-zA-Z]{2,50}$/`

### Meaning
a. `/` - Start a regex
b. `^[a-zA-Z]` - The first name should start with with either small letter or capital letter  
c. `{2,50}$` - The first name should be between two to fifty characters long.
d. `/` - End regex.
 

### Use Case - PHP
`if (preg_match('/^[a-zA-Z]{2,50}$/'),$first_name){`
    //Matches names like Chanda, Chewe, musonda, Mwamba etc
`}`
`else{`
   ` echo 'Your name is invalid. Ensure your first name does not contain spaces'; `
`}`


### Use Case - PHP LARAVEL
`'first_name' => ['regex:/^[a-zA-Z]{2,50}$/'],`





### B. Validating first name and last name only
-There are some cases where you want the user to enter the first name and last name only. This regex will help.
`/^([a-zA-Z]){2,50}\s([a-zA-Z]){2,50}$/`

### Meaning
a. `/` - Start a regex
b. `^([a-zA-Z])` - The first name should start with with either small letter or capital letter  
c. `{2,50}` - The first name should be between two to fifty characters long.
d. `\s` - Allow the user to leave one white space.
e. `[a-zA-Z]` - The surname should start with with either small letter or capital letter.
f. `{2,50}$` - The surname should end between two to fifty characters long.
g. `/` - Close a regex
 

### Use Case - PHP
`if (preg_match('/([a-zA-Z]){2,50}\s([a-zA-Z]){2,50}$/'),$full_name){`
    //Matches names like Chanda Chewe, musonda Mwamba, etc
`}`
`else{`
   ` echo 'Your Full Name is invalid'; `
`}`


### Use Case - PHP LARAVEL
`'first_name' => ['regex:/([a-zA-Z]){2,50}\s([a-zA-Z]){2,50}$/'],`




### C. Validating First name, Last name and Middlename Sometimes
-There are some cases where you want the user to enter the full name with Middlename in between sometimes. This regex seems to work.
`/^([a-zA-Z]){2,256}\s(([a-zA-Z]){2,256}\s)?([a-zA-Z]){2,50}$/`

### Meaning
a. `/` - Start a regex
b. `[a-zA-Z]` - The first name should start with with either small letter or capital letter  
c. `{2,256}` - The first name should be between 2 to 256 characters long .
d. `(([a-zA-Z]){2,256}\s)?` - The question mark at the end implies that there is a possibility of having characters between 2 and 256 here and a white space.
e. `[a-zA-Z]` - The surname should start with with either small letter or capital letter.
f. `{2,50}$` - The surname should end between two to fifty characters long.
g. `/` - Close a regex
 

### Use Case - PHP
`if (preg_match('/^([a-zA-Z]){2,256}\s(([a-zA-Z]){1,256}\s)?([a-zA-Z]){2,50}$/'),$full_names){`
    //Matches names like Chanda henschel Chewe, musonda kalunga Mwamba etc
`}`
`else{`
   ` echo 'Your Full Name is invalid'; `
`}`


### Use Case - PHP LARAVEL
`'first_name' => ['regex:/^([a-zA-Z]){2,256}\s(([a-zA-Z]){1,256}\s)?([a-zA-Z]){2,50}$/'],`






4. ## Password Validations

Common password Validations.

### A. 8 Atleast Characters Long 
-There are some cases where you want to implement a password of length 8 characters or more and ends there. This regex can help
`/^(\d{8,})$/`

### Meaning
a. `/` - Start a regex
b. `^()` - The password should contain...  
c. `\d{8,}$` - More than 8 digits without letters and special characaters.
d. `/` - End regex.
 

### Use Case - PHP
`if (preg_match('/^(\d{8,})$/'),$password){`
    //Matches weak passwords 12345678, 277477388292092, etc
`}`
`else{`
   ` echo 'Your password must contain more than 8 digits'; `
`}`


### Use Case - PHP LARAVEL
`'password' => ['regex:/^(\d{8,})$/'],`





### B. 8 Atleast Characters Long, & Contains Atleast One Uppercase, One Lower Uppercase, A Number, & A Special Character 
- This is the recommended way of passwords implementations. The regex below might help 
`/(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[_@$!%*#?&]).{8,}$/`

### Meaning
a. `/` - Start a regex
b. `?=.*` - should contain atleast...
c. `\d` - Must have atleast one digit. This is equivalent to `[0-9]`;
d. `?=.*` - should contain atleast...
e. `[a-z]` - Must have atleast a lowercase character.
f. `?=.*` - should contain atleast...
g. `[a-z]` - Must have atleast an uppercase character.
h. `?=.*` - should contain atleast...
i. `_@$!%*#?&` - Should contain a special character
j. `.` - It can contain any multiple character
k. `{8,}$` - All characters must be greater than or equal to 8 at end
l. `/` - End regex.
 

### Use Case - PHP
`if (preg_match('/(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[_@$!%*#?&]).{8,}$/'),$password){`
    //Matches strong passwords
`}`
`else{`
   ` echo 'Your password must be 8 characters long and must contain an uppercase, lowecase, number and a special character'; `
`}`


### Use Case - PHP LARAVEL
`'password' => ['regex:/(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[_@$!%*#?&]).{8,}$/'],`



## Contributing

Feel free to make a Pull Request, As long as you are not correcting a spelling. Meaningful PR involves fixing errors and adding more RegExes. 


## Errors

If you discover that a certain ReGex is not working and you are not familiar with ReGex, please raise an Issue on this repo or send an e-mail to Chanda Chewe via [chewec03@gmail.com](mailto:chewec03@gmail.com). All vulnerabilities will be promptly addressed.

## License

This repo is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
