LANDING PAGE + ACCOUNT CREATION PAGE + LOGIN PAGE + RECOVERY PAGE





**System Constraints \& Validation Rules**

UserID Alias: Must be 100% unique. Rule: No English letters. Only Digits and Special Characters allowed.

Email: Mandatory and 100% unique. Used for account recovery.

Password: Length 8–16 characters. Rule: Must start with an alphabet (A-Z/a-z). Can be a duplicate of other users' passwords.

Device Limit: Maximum of 3 accounts per physical Device ID.



**The User Flow (Step-by-Step)**

&#x20;

**Step 1**: The Landing Page (The Welcome) 

The first screen the user sees when they open the app.

**Components**:

App Logo (VURA).

Button 1: "Create Identity" (Leads to Signup).

Button 2: "Sign In" (Leads to Login).

**User** **Action**: User selects whether they are new or returning.



**Step 2:** Account Creation (The Signup)

Pre-Check (Background): When the user clicks "Create Identity," the app silently fetches the DeviceID.

Backend Query: Check if 3 rows already exist for this DeviceID.

Logic: If Count = 3, show Error Popup: "Device Limit Reached." If Count < 3, show the form.

**Input Fields**:

UserID Box: Real-time validation to block letters.

Email Box: Mandatory input.

Password Box: Real-time validation for length and first-letter rule.

**Action**: Click "Secure My Identity."

**Backend**: Save to app\_users table.





**Step 3**: The Login Page (The Gate)

**Input Fields**:

UserID Box (Symbol/Digit input).

Password Box.

**Components**:

Button: "Enter Vura".

Link: "Forgot UserID?"

Link: "Forgot Password?"

**Backend**: Validate credentials. If success, navigate to Main Feed.



**Step 4**: UserID Recovery (The Anchor)

Used when the user forgets their symbol-based ID.

**Input Field**: Email Address.

**Action**: Click "Retrieve My IDs."

**Backend Logic:**

Search database for all user\_id\_alias mapped to that Email.

Trigger Email: "Your Vura UserIDs are: \[list\_of\_ids]."

UI Message: "Check your inbox. If registered, your IDs have been sent."



**Step 5:** Password Reset (The Link)

Used when the user knows their UserID but forgets the password.

Input Fields:

UserID

Email Address

Action: Click "Reset Password."

Backend Logic:

Validate that the provided UserID and Email match the same record.

Trigger Email with a unique reset link.

UI Message: "A password reset link has been sent to your email."



**Screen Component Map (For Frontend Devs)**

|Screen|Components|Primary Actions|
|-|-|-|
|Landing|Logo, SignupBtn, LoginBtn|Navigation|
|Signup	|DeviceIDFetch (Hidden), UserIDInput, EmailInput, PassInput, SubmitBtn	|Data Entry \& Validation|
|Login|UserIDInput, PassInput, LoginBtn, ForgotUIDLink, ForgotPassLink|Authentication|
|Recovery|EmailInput, SendRequestBtn|Email Triggering|

|Reset|UserIDInput, EmailInput, RequestLinkBtn|Email Triggering|
|-|-|-|





**Database Schema (app\_users table)**

id: UUID (Primary Key)

user\_id\_alias: Text (Unique, Index)

email: Text (Index)

password: Text (Hashed)

device\_hash: Text (Index)



TOOL FOR EMAIL SENDING LOGIC : Resend











