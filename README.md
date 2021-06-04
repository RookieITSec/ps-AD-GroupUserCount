# ps-AD-GroupUserCount

This is a three step PowerShell Script to enumerate the AD groups and then count the members of the groups.  This is useful to find groups with no users.  This is also useful to work with very large AD environments.  It could be faster, but hey, it works for now.  I needed to break this into three steps due to the huge size of the domain (~100,000 AD Groups) that resulted in memory running out and the process dying.  

Permissions needed - 
   - I ran this as a regular domain user.  It may run faster on a DC as an Admin.  

Other considerations - 
   - This may set off alarm bells in environments where AD scanning/enumeration can be detected.  
   - Throttling - This script does not throttle, however, the domain settings may limit the response rate.



Details on each step - 

Step 1 - 
This step will use PowerShell to enumerate all Domain Controllers and then provide Ping results to identify what servers respond the fastest.  This could be omitted if you are in a smaller environment where DC load/distance is less of a concern.

Step 2 - 
This step scans the entire AD structure and lists out the AD DC's 

Step 3 - 
The output file from Step2 is used for the input on this step.  This step will read the DN of the AD GRoup, then enumerate the users and count them.  The output is a simple output file with all the detail from the input file with an added column for the counted members.  This only counts the members (groups/users) and does NOT enumerate/count the users who may be given access through nested groups.  
