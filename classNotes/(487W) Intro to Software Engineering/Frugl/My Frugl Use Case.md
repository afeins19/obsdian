n: **User Logs In**
Actor: User

**Trigger**: User launches a  new instance of the application 

**Flow of events:**
1. If User Is auth(), do not auth() and send to home page
2. Present User with an auth page (username/phone number and password). user may log in or change password 
3. User selects log in 
4. credentials are sent to the user database for auth()
5. if auth() send user to home page
6. if not auth() request that user try again 

**Extensions**
	a. The user does not have an account, they will be presented with the option to create an account 
	b. The User forgot their password, the user will be prompted to follow the standard email verification process to reset the password 

**Exceptions**
	a.  the user has entered the incorrect credentials, in this case the user will be notified of this and the "forgot username/password" functions will be presented clearly to the user
	b. the app has trouble communicating with our database due to low/no internet on the users device...notify them of this 
	c. the app has trouble communicating with our internal database due to a server/app issue... notify the user that we are experiencing difficulties
